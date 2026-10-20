---
title: "Exchange, OWA, Credential attacks"
date: 2025-09-22 08:24:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "Common initial access approach is credential attacks against login pages, and Exchange, OWA (Outlook web access) is one of the most targeted in enterprise en…"
media_subpath: /assets/img/tryhackme/2025-09-22-exchange-owa-credential-attacks/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-initial-access/exchange-owa-credential-attacks/
th_id: "soc-lv-2/active-directory/detecting-ad-initial-access/exchange-owa-credential-attacks"
th_parent: "soc-lv-2/active-directory/detecting-ad-initial-access"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-initial-access"]
---

{% include tryhackme-nav.html %}

Common initial access approach is credential attacks against login pages, and Exchange, OWA (Outlook web access) is one of the most targeted in enterprise environments. It's the gateway to corporate email, and it's accessible from the internet by design.

Before we look at credential attacks, we need to be clear about terminology:

- **Exchange** is the server that handles email delivery, calendaring, and contacts.
- **Outlook** is the desktop client application.
- **OWA (Outlook Web Access)** is the browser-based version that runs on IIS.

![image.png](image.png)

- `/owa` is the Outlook Web Access login page. This is where credential attacks happen.
- `/ecp` is the Exchange Control Panel, the administrative interface. Access to this path should be rare and monitored closely, because from there an attacker can create forwarding rules, export mailboxes, or modify Exchange settings.
