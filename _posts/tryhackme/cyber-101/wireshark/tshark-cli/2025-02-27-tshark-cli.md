---
title: "Tshark CLI"
date: 2025-02-27 17:57:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "--export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q"
media_subpath: /assets/img/tryhackme/2025-02-27-tshark-cli/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/tshark-cli/
th_id: "cyber-101/wireshark/tshark-cli"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 17
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

## Statistic

- -z io, phs : protocol hierarchy
- -z endpoints, ip : lọc endpoints theo ip
- -z conv,ip : lọc conversation theo ip
- -z expert : expert info
- -z ptype,tree -q
- **IPv4:** `z ip_hosts,tree -q`
- **IPv6:** `z ipv6_hosts,tree -q`
- IPv4: `z ip_srcdst,tree -q`
- IPv6: `z ipv6_srcdst,tree -q`
- IPv4: `z dests,tree -q`
- IPv6: `z ipv6_dests,tree -q`
- **-z dns,tree -q : DNS**
- **-z http,tree -q**
- -z http2,tree -q

## Stream, Object, Credential

- **Follow Stream**
    - -z follow

![image.png](image.png)

- **Export Objects**
    - --export-objects

![image.png](image%201.png)

 `--export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q`

- **Credentials:**
    - -z credentials -q
