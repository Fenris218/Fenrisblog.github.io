---
title: "Detecting DCSync"
date: 2025-09-28 14:30:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "After the attacker have the highest level of access in the domain. The question is what they do with it."
media_subpath: /assets/img/tryhackme/2025-09-28-detecting-dcsync/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-credential-attacks/detecting-dcsync/
th_id: "soc-lv-2/active-directory/detecting-ad-credential-attacks/detecting-dcsync"
th_parent: "soc-lv-2/active-directory/detecting-ad-credential-attacks"
th_kind: note
th_order: 4
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-credential-attacks"]
---

{% include tryhackme-nav.html %}

After the attacker have the highest level of access in the domain. The question is what they do with it.

Attackers target DCSync because it lets them extract every password hash in the domain without touching the domain controller's disk, without creating volume shadow copies, and without needing physical access to the DC. 

It works by abusing the Active Directory replication protocol (DRSUAPI), the same protocol that legitimate domain controllers use to synchronize directory data with each other. The attacker's machine pretends to be a domain controller and requests password data via DRSUAPI. If their account has the right permissions, the real DC complies. Domain Admins, Enterprise Admins, and DC machine accounts have these replication rights by default.
