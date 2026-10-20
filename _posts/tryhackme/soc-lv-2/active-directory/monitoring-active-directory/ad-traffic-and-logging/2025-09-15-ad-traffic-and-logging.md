---
title: "AD Traffic and Logging"
date: 2025-09-15 13:17:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: ""
media_subpath: /assets/img/tryhackme/2025-09-15-ad-traffic-and-logging/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/monitoring-active-directory/ad-traffic-and-logging/
th_id: "soc-lv-2/active-directory/monitoring-active-directory/ad-traffic-and-logging"
th_parent: "soc-lv-2/active-directory/monitoring-active-directory"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/monitoring-active-directory"]
---

{% include tryhackme-nav.html %}

## **Protocol Summary**

| **Protocol** | **Ports** | **What It Does** | **Normal Usage** |
| --- | --- | --- | --- |
| Kerberos | 88 | Default authentication in AD | User logins, service access, ticket requests |
| LDAP | 389, 636, 3268, 3269 | Directory queries and modifications | User lookups, group membership checks, and address book queries |
| SMB | 445 (139 for legacy NetBIOS sessions) | File sharing, remote administration | Accessing shared folders, printers, and administrative tools |
| RDP | 3389 | Interactive remote desktop | Help desk support, server administration |
| Name Resolution (Legacy) | 137, 138, 5355 | NetBIOS (TCP/UDP - 137/138) and LLMNR (5355) | Fallback when DNS fails, for older applications |
