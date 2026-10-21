---
title: "CDN and IP visibility"
date: 2025-10-15 19:47:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Traffic Analysis"]
tags: ["tryhackme", "advanced-traffic-analysis"]
description: "When WKST-FINANCE-04 connected to 172.67.153.42, our logs recorded the source IP, destination IP, port, and byte count. What they did not record is which ser…"
media_subpath: /assets/img/tryhackme/2025-10-15-cdn-and-ip-visibility/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-traffic-analysis/cdn-and-ip-visibility/
th_id: "soc-lv-2/advanced-traffic-analysis/cdn-and-ip-visibility"
th_parent: "soc-lv-2/advanced-traffic-analysis"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-traffic-analysis"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-traffic-analysis"]
---

{% include tryhackme-nav.html %}

![image.png](image.png)

## **The CDN Visibility Problem**

When WKST-FINANCE-04 connected to `172.67.153.42`, our logs recorded the source IP, destination IP, port, and byte count. What they did not record is which service the traffic was actually destined for - that Cloudflare address simultaneously proxies traffic for millions of distinct services. Our logs show us the CDN hop. They cannot show us what is behind it.

This is why IP reputation returns clean, and blocking is not an option. The IP is not malicious. It is shared infrastructure. Detection requires a different approach.

## **Why IP-Based Monitoring Fails Against CDNs**

Traditional IP reputation was built on a simpler assumption: one IP, one organization. CDNs invalidated that entirely. A single Cloudflare anycast address simultaneously proxies traffic for millions of distinct services, which is why no reputation feed will ever flag it, as blocking it would take down legitimate access for all of them. The four CDN providers we will encounter most often in enterprise traffic:

| **CDN Provider** | **ASN** | **Representative IP Ranges** |
| --- | --- | --- |
| Cloudflare | AS13335 | 173.245.48.0/20, 103.21.244.0/22, 103.22.200.0/22, 103.31.4.0/22, 141.101.64.0/18, 108.162.192.0/18, 190.93.240.0/20, 188.114.96.0/20, 197.234.240.0/22, 198.41.128.0/17, 162.158.0.0/15, 104.16.0.0/13, 104.24.0.0/14, 172.64.0.0/13, 131.0.72.0/22 — [full list(opens in new tab)](https://www.cloudflare.com/ips-v4/) |
| Fastly | AS54113 | 151.101.0.0/16 |
| Akamai | AS16625 | 23.32.0.0/11 |
| AWS CloudFront | AS16509 | 13.32.0.0/15, 52.84.0.0/15 |

## **How Attackers Exploit CDN Infrastructure**

Attackers exploit the same properties that make CDNs useful: shared infrastructure, clean reputation, and encrypted traffic. Two techniques appear consistently across enterprise incidents.

**1) Domain Fronting**

Domain fronting ([MITRE ATT&CK T1090.004(opens in new tab)](https://attack.mitre.org/techniques/T1090/004/)) exploits the gap between the TLS SNI field (which advertises a legitimate hostname like `www.microsoft.com`) and the HTTP Host header inside the encrypted session, which routes traffic to attacker-controlled infrastructure. Every observable indicator points to a trusted domain while the actual C2 traffic hides inside the encrypted payload. 

**2) CDN Tunneling and Worker Abuse**

Where domain fronting has been restricted, attackers have moved to Cloudflare Workers and Cloudflare Tunnel, exposing C2 services through `*.workers.dev` and `*.trycloudflare.com`, both domains **allowlisted** by most content filters. [BlackWater Cloudflare Workers(opens in new tab)](https://www.bleepingcomputer.com/news/security/blackwater-malware-abuses-cloudflare-workers-for-c2-communication/) **used Cloudflare Workers as a C2 relay; [SerpentineCloud (2025)(opens in new tab)](https://www.proofpoint.com/us/blog/threat-insight/threat-actor-abuses-cloudflare-tunnels-deliver-rats) routes C2 through Cloudflare Tunnel endpoints in organizations that had **allowlisted** `*.trycloudflare.com`.

## **The Investigative Pivot: What to Look at When IP Is Meaningless**

**1) ASN Enrichment**

Before we narrow down to a specific connection, let's get a picture of where all outbound traffic is actually going. We will use the `asn_lookup` table, which enriches each destination IP with its ASN, organization name, traffic category, and risk tier at query time. ASN enrichment does not reveal which domain is behind a CDN IP address. What it tells us is the type of organization that operates the destination infrastructure. Traffic to Cloudflare CDN is expected. Traffic to Bulletproof Hosting or a Tor exit node requires immediate attention, regardless of IP reputation. 

**Search Query:**

```
index=lab sourcetype=fortigate_traffic
| lookup asn_lookup network AS dstip OUTPUT dst_asn_org dst_category dst_risk
| --- |
| stats count by dst_category dst_asn_org
| sort -count
```

**2) Behavioral Baselines**

A CDN IP in isolation tells us nothing. What matters is the traffic pattern around it. Three signals can indicate C2 activity through CDN infrastructure. Each comes with caveats worth understanding before escalating:

- **Beaconing regularity:** Connections to the same CDN IP at fixed intervals with no corresponding user activity.
- **Asymmetric volume:** High outbound byte counts without proportional inbound responses. A CDN serving legitimate content returns substantially more data than it receives. C2 exfiltration inverts this ratio.
- **Off-hours persistence:** Connections continuing overnight or during hours when the host user is inactive. Legitimate CDN requests follow user sessions; C2 beacons are indifferent to whether anyone is logged in. Confirming which process is responsible at scale requires Sysmon EventID 3 deployed across the estate.

**Search Query:**

```
index=lab sourcetype=fortigate_traffic srcip=10.10.15.44 dstip=172.67.153.42
| eval hour=strftime(_time,"%Y-%m-%d %H")
| --- |
| stats count as per_hour min(sentbyte) as min_b max(sentbyte) as max_b by hour
| sort -per_hour | head 15
```
