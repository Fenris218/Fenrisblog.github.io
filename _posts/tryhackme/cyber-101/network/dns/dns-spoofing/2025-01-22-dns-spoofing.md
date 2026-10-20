---
title: "DNS Spoofing"
date: 2025-01-22 17:21:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "This is a powerful technique for launching a Man-in-the-Middle (MITM) attack. Here's how it works:"
media_subpath: /assets/img/tryhackme/2025-01-22-dns-spoofing/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/dns/dns-spoofing/
th_id: "cyber-101/network/dns/dns-spoofing"
th_parent: "cyber-101/network/dns"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/network", "cyber-101/network/dns"]
---

{% include tryhackme-nav.html %}

This is a powerful technique for launching a **Man-in-the-Middle (MITM)** attack. Here's how it works:

1. **The Victim** tries to visit their bank at `my-real-bank.com`.
2. **The Attacker**, who is already on the local network (perhaps via ARP spoofing), intercepts the victim's  DNS query.
3. **The Spoof:** The attacker quickly sends a **fake DNS response** to the victim. This fake response says, `my-real-bank.com` is at my IP address: `ATTACKER_IP`.
4. **The Interception:** The victim's computer trusts this fake response and saves it in its DNS cache. When the victim tries to connect to their bank, they unknowingly connect directly to the attacker's server, which might host a perfect replica of the real banking site.

## **Indicators of the Attack**

We can look for the following key indicators while investigating the logs or network traffic for a potential Man-in-the-Middle attack using DNS spoofing.

- **Multiple DNS responses for the same query**
- **DNS response from an unexpected source**: A DNS reply arrives from an IP address **that does not match any configured resolver** (like 8.8.8.8 or your  DNS server).
- **Suspiciously short TTL (Time-To-Live) values**: Attackers use very low TTLs (1 - 30s) to keep poisoned entries short-lived and reassert control.
- **Unsolicited DNS responses**

### Filter

- `dns.flags.response == 1 && ip.src == 8.8.8.8` (Legitimate DNS servers (like Google’s `8.8.8.8`) respond from a known external IP address. By filtering responses from this IP, we can see what `normal` answers look like for comparison.)
- `dns && [dns.qry.name](http://dns.qry.name/) == "corp-login.acme-corp.local"`
