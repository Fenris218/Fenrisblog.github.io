---
title: "Detecting SMB lateral Movement"
date: 2025-10-03 19:35:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "Windows systems maintain default Administrative Shares (C$, ADMIN$, IPC$) created by the Server service at boot. These shares leverage the SMB protocol (Port…"
media_subpath: /assets/img/tryhackme/2025-10-03-detecting-smb-lateral-movement/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-lateral-movement/detecting-smb-lateral-movement/
th_id: "soc-lv-2/active-directory/detecting-ad-lateral-movement/detecting-smb-lateral-movement"
th_parent: "soc-lv-2/active-directory/detecting-ad-lateral-movement"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-lateral-movement"]
---

{% include tryhackme-nav.html %}

## **Admin Shares**

Windows systems maintain default **Administrative Shares** (`C$`, `ADMIN$`, `IPC$`) created by the **Server service** at boot. These shares leverage the **SMB protocol** (Port 445) to allow remote management:

- `C$`: Maps to the root of the system drive; additional drives follow the same pattern (`D$`, `E$`, etc.).
- `ADMIN$`: Points to `%SystemRoot%` (typically `C:\Windows`).
- `IPC$`: A logical share for Inter-Process Communication via named pipes, essential for remote RPC calls.

Regular users don't access these during normal work. They use named shares like Marketing, Shared, or IT. When we see admin share access, it's either an administrator doing maintenance or an attacker moving laterally.

- Eventlog : 5140 , 4624
