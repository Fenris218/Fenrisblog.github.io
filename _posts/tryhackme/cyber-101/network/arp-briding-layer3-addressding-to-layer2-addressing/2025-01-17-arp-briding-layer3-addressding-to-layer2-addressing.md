---
title: "ARP: briding Layer3 Addressding to Layer2 Addressing"
date: 2025-01-17 12:16:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "Address Resolution Protocol (ARP) makes it possible to find the MAC address of another device on the Ethernet. In the example below, a host with the IP addre…"
media_subpath: /assets/img/tryhackme/2025-01-17-arp-briding-layer3-addressding-to-layer2-addressing/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing/
th_id: "cyber-101/network/arp-briding-layer3-addressding-to-layer2-addressing"
th_parent: "cyber-101/network"
th_kind: note
th_order: 7
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 1
th_ancestors: ["cyber-101", "cyber-101/network"]
---

{% include tryhackme-nav.html %}

- Remember that the two common data link layers we use are Ethernet (IEEE 802.3) and WiFi (IEEE 802.11). Whenever one host needs to communicate with another host on the same Ethernet or WiFi, it must send the IP packet within a data link layer frame. Although it knows the IP address of the target host, it needs to look up the target’s MAC address so the proper data link header can be created ⇒ two devices on the same Ethernet cannot communicate without knowing each other’s MAC addresses.
- Address Resolution Protocol (ARP) makes it possible to find the MAC address of another device on the Ethernet.

Address Resolution Protocol (ARP) makes it possible to find the MAC address of another device on the Ethernet. In the example below, a host with the IP address `192.168.66.89` wants to communicate with another system with the IP address `192.168.66.1`. It sends an ARP Request asking the host with the IP address `192.168.66.1` to respond. The ARP Request is sent from the MAC address of the requester to the broadcast MAC address, `ff:ff:ff:ff:ff:ff` as shown in the first packet. The ARP Reply arrived shortly afterwards, and the host with the IP address `192.168.66.1` responded with its MAC address. From this point, the two hosts can exchange data link layer frames.

Terminal

```bash
user@TryHackMe$ tshark -r arp.pcapng -Nn    1 0.000000000 cc:5e:f8:02:21:a7 → ff:ff:ff:ff:ff:ff ARP 42 Who has 192.168.66.1? Tell 192.168.66.89
    2 0.003566632 44:df:65:d8:fe:6c → cc:5e:f8:02:21:a7 ARP 42 192.168.66.1 is at 44:df:65:d8:fe:6c
```

If we use `tcpdump`, the packets will be displayed differently. It uses the terms ARP **Request** and ARP **Reply**. For your information, the output is shown in the terminal below.

Terminal

```bash
user@TryHackMe$ tcpdump -r arp.pcapng -n -v17:23:44.506615 ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.66.1 tell 192.168.66.89, length 28
17:23:44.510182 ARP, Ethernet (len 6), IPv4 (len 4), Reply 192.168.66.1 is-at 44:df:65:d8:fe:6c, length 28
```

An ARP Request or ARP Reply is not encapsulated within a UDP or even IP packet; it is encapsulated directly within an Ethernet frame. The following ARP Reply shows this.

![Wireshark showing an ARP Reply encapsulated directly within an Ethernet frame.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849185596.png)

ARP is considered layer 2 because it deals with MAC addresses. Others would argue that it is part of layer 3 because it supports IP operations. What is essential to know is that ARP allows the translation from layer 3 addressing to layer 2 addressing.

