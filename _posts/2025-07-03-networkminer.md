---
title: "NetworkMiner"
date: 2025-07-03 11:03:00 +0700
categories: ["TryHackMe", "SOC LV1", "NetworkMiner"]
tags: ["tryhackme", "networkminer"]
description: "Gần giống Wireshark, NetworkMiner can be used as a passive network sniffer/packet capturing tool to detect operating systems, sessions, hostnames, open ports…"
media_subpath: /assets/img/tryhackme/2025-07-03-networkminer/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/networkminer/
th_id: "soc-lv1/networkminer"
th_parent: "soc-lv1"
th_kind: module
th_order: 11
th_course: "soc-lv1"
th_module: "soc-lv1/networkminer"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

Gần giống Wireshark, NetworkMiner can be used as a passive network sniffer/packet capturing tool to detect operating systems, sessions, hostnames, open ports etc. without putting any traffic on the network. NetworkMiner can also parse PCAP files for off-line analysis and to regenerate/reassemble transmitted files and certificates from PCAP files.

### **Pros and Cons**

As mentioned in the previous task, NetworkMiner is mainly used to gain an overview of the network. Before starting to investigate traffic data, let's look at **the pros and cons of the NetworkMiner.**

**Pros**

- OS fingerprinting
- Easy file extraction
- Credential grabbing
- Clear text keyword parsing
- Overall overview

**Cons**

- Not useful in active sniffing
- Not useful for large pcap investigation
- Limited filtering
- Not built for manual traffic investigation

## **Differences Between Wireshark and NetworkMiner**

The best practice is to record the traffic for offline analysis, quickly overview the pcap with NetworkMiner and go deep with Wireshark for further investigation.

| **Feature** | **NetworkMiner** | **Wireshark** |
| --- | --- | --- |
| Purpose | Quick overview, traffic mapping, and data extraction | In-Depth analysis |
| GUI | ✅ | ✅ |
| Sniffing | ✅ | ✅ |
| Handling PCAPS | ✅ | ✅ |
| OS Fingerprinting | ✅ | ❌ |
| Parameter/Keyword Discovery | ✅ | Manual |
| Credential Discovery | ✅ | ✅ |
| File Extraction | ✅ | ✅ |
| Filtering Options | Limited | ✅ |
| Packet Decoding | Limited | ✅ |
| Protocol Analysis | ❌ | ✅ |
| Payload Analysis | ❌ | ✅ |
| Statistical Analysis | ❌ | ✅ |
| Cross-Platform Support | ✅ | ✅ |
| Host Categorisation | ✅ | ❌ |
| Ease of Management | ✅ | ✅ |
