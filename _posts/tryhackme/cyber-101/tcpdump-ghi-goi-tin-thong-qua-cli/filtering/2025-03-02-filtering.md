---
title: "Filtering"
date: 2025-03-02 08:00:00 +0700
categories: ["TryHackMe", "Cyber 101", "TCPdump : ghi gói tin thông qua CLI"]
tags: ["tryhackme", "tcpdump-ghi-goi-tin-thong-qua-cli"]
description: "Let’s say you are only interested in IP packets exchanged with your network printer or a specific game server. You can easily limit the captured packets to t…"
media_subpath: /assets/img/tryhackme/2025-03-02-filtering/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli/filtering/
th_id: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli/filtering"
th_parent: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"]
---

{% include tryhackme-nav.html %}

### Filtering by Host

Let’s say you are only interested in IP packets exchanged with your network printer or a specific game server. You can easily limit the captured packets to this host using `host IP` or `host HOSTNAME`. In the terminal below, we capture all the packets exchanged with `example.com` and save them to `http.pcap`. It is important to note that capturing packets requires you to be logged-in as `root` or to use `sudo`

![image.png](image.png)

**Filtering by Port**

If you want to capture all DNS traffic, you can limit the captured packets to those on `port 53`. Remember that DNS uses UDP and TCP ports 53 by default.

![image.png](image%201.png)

You can limit the packets to those from a particular source port number or to a particular destination port number using `src port PORT_NUMBER` and `dst port PORT_NUMBER`, respectively.

### Filtering by Protocol

The final type of filtering we will cover is filtering by protocol. You can limit your packet capture to a specific protocol; examples include: `ip`, `ip6`, `udp`, `tcp`, and `icmp`

![image.png](image%202.png)

### Logical Operators

Three logical operators that can be handy:

- `and`: Captures packets where both conditions are true. For example, `tcpdump host 1.1.1.1 and tcp` captures `tcp` traffic with `host 1.1.1.1`.
- `or`: Captures packets when either one of the conditions is true. For instance, `tcpdump udp or icmp` captures UDP or ICMP traffic.
- `not`: Captures packets when the condition is not true. For example, `tcpdump not tcp` captures all packets except TCP segments; we expect to find UDP, ICMP, and ARP packets among the results.
