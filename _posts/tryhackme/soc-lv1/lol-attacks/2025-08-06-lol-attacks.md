---
title: "LOL Attacks"
date: 2025-08-06 09:37:00 +0700
categories: ["TryHackMe", "SOC LV1", "LOL Attacks"]
tags: ["tryhackme", "lol-attacks"]
description: "Living Off the Land methods are not limited to Windows; similar approaches exist on Unix and Linux, and public collections document common patterns for both…"
media_subpath: /assets/img/tryhackme/2025-08-06-lol-attacks/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/lol-attacks/
th_id: "soc-lv1/lol-attacks"
th_parent: "soc-lv1"
th_kind: module
th_order: 23
th_course: "soc-lv1"
th_module: "soc-lv1/lol-attacks"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

## 1. LOL tools

- Powershell
- WMIC or WMI : is used to run commands locally or on remote hosts and to query system state.
- **Certutil** is used to fetch files and encode or decode payloads.
- **Mshta** is used to run HTA content or an inline script delivered by a document or link.
- **Rundll32** is used to invoke  DLL exports or trigger URL handlers.
- **Scheduled tasks** (**schtasks**) are used to run code at logon or on a schedule for persistence

Living Off the Land methods are not limited to Windows; similar approaches exist on Unix and Linux, and public collections document common patterns for both platforms, for example, [LOLBAS (opens in new tab)](https://lolbas-project.github.io/)for Windows and [GTFOBins (opens in new tab)](https://gtfobins.github.io/)for Unix.
