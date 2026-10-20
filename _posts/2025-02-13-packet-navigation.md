---
title: "Packet Navigation"
date: 2025-02-13 15:43:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: ""
media_subpath: /assets/img/tryhackme/2025-02-13-packet-navigation/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/packet-navigation/
th_id: "cyber-101/wireshark/packet-navigation"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 5
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

- Goto packet : Ctrl + g
- Find packet :  Wireshark can find packets by packet content. You can use the **"Edit --> Find Packet"** menu to make a search inside the packets for a particular event of interest.
    - The first is knowing the input type: Display filter, Hex, String, Regex
    - The second point is choosing the search field: You can conduct searches in the three panes (packet list, packet details, and packet bytes)
