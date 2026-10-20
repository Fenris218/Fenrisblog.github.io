---
title: "Expert Info"
date: 2025-02-14 16:44:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "You can use the \"lower left bottom section\" in the status bar or \"Analyse --> Expert Information\" menu to view all available information entries via a dialog…"
media_subpath: /assets/img/tryhackme/2025-02-14-expert-info/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/expert-info/
th_id: "cyber-101/wireshark/expert-info"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 6
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

You can use the **"lower left bottom section"** in the status bar or **"Analyse --> Expert Information"** menu to view all available information entries via a dialogue box. It will show the packet number, summary, group protocol and total occurrence.

![Wireshark - expert info](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31917b6f1e846d3383218cabf1c07caf.png)

Expert info can provide a group of categories in three different severities. Details are shown in the table below.

| **Severity** | **Colour** | **Info** |
| --- | --- | --- |
| **Chat** | **Blue** | Information on usual workflow. |
| **Note** | **Cyan** | Notable events like application error codes. |
| **Warn** | **Yellow** | Warnings like unusual error codes or problem statements. |
| **Error** | **Red** | Problems like malformed packets. |

Frequently encountered information groups are listed in the table below. You can refer to [Wireshark's official documentation](https://www.wireshark.org/docs/) for more information on the expert information entries.

| **Group** | **Info** | **Group** | **Info** |
| --- | --- | --- | --- |
| **Checksum** | Checksum errors | **Deprecated** | Deprecated protocol usage |
| **Comment** | Packet comment detection | **Malformed** | Malformed packet detection |
