---
title: "Tunneling Traffic: DNS and ICMP"
date: 2025-02-22 12:52:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "Usually, ICMP tunnelling attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. As the ICMP packets can transfer a…"
media_subpath: /assets/img/tryhackme/2025-02-22-tunneling-traffic-dns-and-icmp/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/tunneling-traffic-dns-and-icmp/
th_id: "cyber-101/wireshark/tunneling-traffic-dns-and-icmp"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 12
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

### **ICMP Analysis**

Usually, ICMP tunnelling attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. As the ICMP packets can transfer an additional data payload, adversaries use this section to exfiltrate data and establish a C2 connection. It could be a TCP, HTTP or SSH data. As the ICMP protocols provide a great opportunity to carry extra data, it also has disadvantages. Most enterprise networks block custom packets or require administrator privileges to create custom ICMP packets.

A large volume of ICMP traffic or anomalous packet sizes are indicators of ICMP tunnelling. Still, the adversaries could create custom packets that match the regular ICMP packet size (64 bytes), so it is still cumbersome to detect these tunnelling activities. However, a security analyst should know the normal and the abnormal to spot the possible anomaly and escalate it for further analysis.

| **Notes** | **Wireshark filters** |
| --- | --- |
| Global search | • `icmp` |
| **"ICMP" options for grabbing the low-hanging fruits:**<br>• Packet length.<br>• ICMP destination addresses.<br>• Encapsulated protocol signs in ICMP payload. | • `data.len > 64 and icmp` |

```bash
(data.len > 64) and (icmp contains "ssh" or icmp contains "ftp" or icmp contains "tcp" or icmp contains "http")
```

## DNS Analysis

As it is the essential part of web services, it is commonly used and trusted, and therefore often ignored. Due to that, adversaries use it in data exfiltration and C2 activities.

DNS attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. Adversary creates (or already has) a domain address and configures it as a C2 channel. The malware or the commands executed after exploitation sends DNS queries to the C2 server. However, these queries are longer than default DNS queries and crafted for subdomain addresses. Unfortunately, these subdomain addresses are not actual addresses; they are encoded commands as shown below:

**"encoded-commands.maliciousdomain.com"**

When this query is routed to the C2 server, the server sends the actual malicious commands to the host. As the DNS queries are a natural part of the networking activity, these packets have the chance of not being detected by network perimeters. A security analyst should know how to investigate the DNS packet lengths and target addresses to spot these anomalies.

| **Notes** | **Wireshark Filter** |
| --- | --- |
| Global search | • `dns` |
| **"DNS" options for grabbing the low-hanging fruits:**<br>• Query length.<br>• Anomalous and non-regular names in DNS addresses.<br>• Long DNS addresses with encoded subdomain addresses.<br>• Known patterns like dnscat and dns2tcp. ( tool dùng để tunneling)<br>• Statistical analysis like the anomalous volume of DNS requests for a particular target.<br>**!mdns:** Disable local link device queries. ( để focus vào các dns ra internet) | • `dns contains "dnscat"`<br>• `dns.qry.name.len > 15 and !mdns` |

*mDNS (multicast DNS ): is a [computer networking protocol](https://en.wikipedia.org/wiki/Computer_networking_protocol) that resolves [hostnames](https://en.wikipedia.org/wiki/Hostname) to IP addresses within small networks that do not include a local [name server](https://en.wikipedia.org/wiki/Name_server). When an mDNS client needs to resolve a hostname, it sends an [IP multicast](https://en.wikipedia.org/wiki/IP_multicast) query message that asks the host having that name to identify itself. That target machine then multicasts a message that includes its IP address. All machines in that [subnet](https://en.wikipedia.org/wiki/Subnet) can then use that information to update their mDNS [caches](https://en.wikipedia.org/wiki/Cache_(computing)). Any host can relinquish its claim to a name by sending a response packet with a [time to live](https://en.wikipedia.org/wiki/Time_to_live) (TTL) equal to zero.

By default, mDNS exclusively resolves hostnames ending with the [`.local`](https://en.wikipedia.org/wiki/.local) top-level domain. This can cause problems if `.local` includes hosts that do not implement mDNS but that can be found via a conventional unicast DNS server. Resolving such conflicts requires network-configuration changes that mDNS was designed to avoid.
