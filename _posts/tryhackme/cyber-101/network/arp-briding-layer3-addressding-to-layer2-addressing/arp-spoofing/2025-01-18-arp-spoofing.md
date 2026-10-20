---
title: "ARP Spoofing"
date: 2025-01-18 13:17:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "In ARP spoofing, an attacker sends fake ARP replies to trick devices into associating the attacker’s MAC address with a legitimate IP, usually the default ga…"
media_subpath: /assets/img/tryhackme/2025-01-18-arp-spoofing/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing/arp-spoofing/
th_id: "cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing/arp-spoofing"
th_parent: "cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/network", "cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing"]
---

{% include tryhackme-nav.html %}

In ARP spoofing, an attacker sends fake ARP replies to trick devices into associating the attacker’s MAC address with a legitimate IP, usually the default gateway. This allows the attacker to intercept, modify, or redirect traffic.

### **Why ARP Spoofing Works**

ARP has **no authentication**. Bất kỳ thiết bị nào cũng có thể gửi unsolicited `is-at` messages. An attacker exploits this vulnerability by sending fake ARP replies to victims and gateways:

- `192.16.10.100` is at `02:fe:BB:cd:55:55` attacker claims to be the gateway.

**Results:**

- The Victim's ARP cache becomes poisoned.
- All traffic intended for the gateway flows through the attacker first (MITM).

## **Indicators of the Attack**

We can look for the following key indicators while investigating the logs or network traffic for a potential Man-in-the-Middle attack using ARP spoofing.

- **Duplicate MAC-to-IP Mappings**: Multiple MAC addresses claiming the same IP address. Indicates impersonation.
- **Unsolicited ARP Replies**: High number of ARP replies without matching requests ("gratuitous ARP").
- **Abnormal ARP Traffic Volume:** A Large number of ARP packets in short intervals.
- **Unusual Traffic Routing**: Traffic rerouted through the attacker’s MAC.
- **Gateway Redirection Patterns:** Multiple destination MACs for the same gateway IP.
- **ARP Probe / Reply Loops**: Many ARP requests with `Who has 192.168.1.x? Tell 192.168.1.y` patterns.

https://tryhackme.com/room/mitmdetection?taskNo=4&sharerId=6704a924d9503f79da2f5690

### Filter

- arp.opcode==1 : ARP request
- arp.opcode==2 : ARP response (Forged ARP poisoning typically uses unsolicited `is-at` replies (gratuitous/unasked replies). These are strong indicators)
- arp.isgratuitous : hiển thị các gói gratuitious
- arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1 (IP default gateway) : filter như này có thể thấy các MAC khác nhau cùng tự nhận là IP 192.168.10.1 của mình (default gateway)

![image.png](image.png)
