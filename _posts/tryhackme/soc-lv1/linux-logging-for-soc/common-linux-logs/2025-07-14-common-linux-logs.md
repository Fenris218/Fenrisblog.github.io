---
title: "Common Linux Logs"
date: 2025-07-14 10:14:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logging for SOC"]
tags: ["tryhackme", "linux-logging-for-soc"]
description: "~/.bash_history là file lưu sau mỗi phiên user log out của mỗi user, tuy nhiên nó không track non-interactive commands ( như cron jobs, web severs,..) và có…"
media_subpath: /assets/img/tryhackme/2025-07-14-common-linux-logs/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logging-for-soc/common-linux-logs/
th_id: "soc-lv1/linux-logging-for-soc/common-linux-logs"
th_parent: "soc-lv1/linux-logging-for-soc"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logging-for-soc"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logging-for-soc"]
---

{% include tryhackme-nav.html %}

- `/var/log/kern.log`: Kernel messages and errors, useful for more advanced investigations
- `/var/log/syslog (or /var/log/messages)`: A consolidated stream of various Linux events
- `/var/log/dpkg.log (or /var/log/apt)`: Package manager logs on Debian-based systems
- `/var/log/dnf.log (or /var/log/yum.log)`: Package manager logs on RHEL-based systems

## Bash history

`~/.bash_history`  là file lưu sau mỗi phiên user log out của mỗi user, tuy nhiên nó không track non-interactive commands ( như cron jobs, web severs,..) và có một số vấn đề

![image.png](image.png)

- Lệnh history : hiện lịch sử command trong shell hiện tại
