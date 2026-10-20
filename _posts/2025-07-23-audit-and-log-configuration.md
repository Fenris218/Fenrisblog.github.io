---
title: "Audit and Log Configuration"
date: 2025-07-23 19:23:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Hardening"]
tags: ["tryhackme", "linux-hardening"]
description: ""
media_subpath: /assets/img/tryhackme/2025-07-23-audit-and-log-configuration/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-hardening/audit-and-log-configuration/
th_id: "soc-lv1/linux-hardening/audit-and-log-configuration"
th_parent: "soc-lv1/linux-hardening"
th_kind: note
th_order: 5
th_course: "soc-lv1"
th_module: "soc-lv1/linux-hardening"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-hardening"]
---

{% include tryhackme-nav.html %}

- `/var/log/messages` - a general log for Linux systems
- `/var/log/auth.log` - a log file that lists all authentication attempts (Debian-based systems)
- `/var/log/secure` - a log file that lists all authentication attempts (Red Hat and Fedora-based systems)
- `/var/log/utmp` - an access log that contains information regarding users that are currently logged into the system
- `/var/log/wtmp` - an access log that contains information for all users that have logged in and out of the system
- `/var/log/kern.log` - a log file containing messages from the kernel
- `/var/log/boot.log` - a log file that contains start-up messages and boot information
