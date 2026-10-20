---
title: "Colouring packets"
date: 2025-02-09 11:39:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "Along with quick packet information, Wireshark also colour packets in order of different conditions and the protocol to spot anomalies and protocols in captu…"
media_subpath: /assets/img/tryhackme/2025-02-09-colouring-packets/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/colouring-packets/
th_id: "cyber-101/wireshark/colouring-packets"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

## **Colouring Packets**

Along with quick packet information, Wireshark also colour packets in order of different conditions and the protocol to spot anomalies and protocols in captures quickly (this explains why almost everything is green in the given screenshots). This glance at packet information can help track down exactly what you're looking for during analysis. You can create custom colour rules to spot events of interest by using display filters, and we will cover them in the next room. Now let's focus on the defaults and understand how to view and use the represented data details.

Wireshark has two types of packet colouring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. You can use the "right-click menu" or **"View --> Coloring Rules"** menu to create permanent colouring rules. The **"Colourise Packet List"** menu activates/deactivates the colouring rules. Temporary packet colouring is done with the "right-click menu" or **"View --> Conversation Filter"** menu, which is covered in TASK-5.

The default permanent colouring is shown below.

![Wireshark - packet colours](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1760957486290.svg)
