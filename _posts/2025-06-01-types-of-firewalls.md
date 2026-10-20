---
title: "Types of Firewalls"
date: 2025-06-01 15:31:00 +0700
categories: ["TryHackMe", "Cyber 101", "Firewall"]
tags: ["tryhackme", "firewall"]
description: ""
media_subpath: /assets/img/tryhackme/2025-06-01-types-of-firewalls/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/firewall-2/types-of-firewalls/
th_id: "cyber-101/firewall-2/types-of-firewalls"
th_parent: "cyber-101/firewall-2"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/firewall-2"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/firewall-2"]
---

{% include tryhackme-nav.html %}

- Có nhiều cách để phân loại firewall :
    - Hardware - Software
    - Personal - Commercial
- Before we classify firewalls based on their abilities, it is worthy of remembering that firewalls focus on layers 3 and 4 and, to a lesser extent, layer 2. Next-generation firewalls are also designed to cover layers 5, 6, and 7. The more layers a firewall can inspect, the more sophisticated it gets and the more processing power it needs.
    - Packet-Filtering Firewall
    - Circuit-Level Gateway: thêm lớp kiểm tra TCp three-way-handshake
    - Stateful Inspection Firewall : kiểm tra session
    - Proxy Firewall
    - Next-Generation Firewall : Có thể kiểm tra từ layer2-7
    - Cloud Firewall or Firewall as a Service : FWaaS replaces a hardware firewall in a cloud environment. Its features might be comparable to NGFW
