---
title: "Understand IIS and its log"
date: 2025-09-20 18:22:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "What IIS Is and Why It Matters"
media_subpath: /assets/img/tryhackme/2025-09-20-understand-iis-and-its-log/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-initial-access/understand-iis-and-its-log/
th_id: "soc-lv-2/active-directory/detecting-ad-initial-access/understand-iis-and-its-log"
th_parent: "soc-lv-2/active-directory/detecting-ad-initial-access"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-initial-access"]
---

{% include tryhackme-nav.html %}

**What IIS Is and Why It Matters**

IIS là webserver Microsoft's web server platform.  Exchange, SharePoint, ADFS, and many internal business applications all run on IIS. Any of these applications can become an initial access point if an attacker finds a vulnerability to exploit.

![image.png](image.png)

## **IIS Log Basics**

IIS stores access logs in `C:\inetpub\logs\LogFiles\W3SVC1` by default

![image.png](image%201.png)
