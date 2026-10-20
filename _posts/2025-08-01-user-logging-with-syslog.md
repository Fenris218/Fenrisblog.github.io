---
title: "User Logging With Syslog"
date: 2025-08-01 16:32:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logs Investigations"]
tags: ["tryhackme", "linux-logs-investigations"]
description: "Syslog consists of three main components:"
media_subpath: /assets/img/tryhackme/2025-08-01-user-logging-with-syslog/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logs-investigations/user-logging-with-syslog/
th_id: "soc-lv1/linux-logs-investigations/user-logging-with-syslog"
th_parent: "soc-lv1/linux-logs-investigations"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logs-investigations"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logs-investigations"]
---

{% include tryhackme-nav.html %}

Syslog consists of three main components:

1. **Syslog daemon**: The `rsyslogd` daemon (or `syslogd` in older systems) handles logging and routing messages.
2. **Configuration file**: The `/etc/rsyslog.conf` file (or `/etc/syslog.conf`) defines rules for logging, including log file locations, filtering, and message forwarding.
3. **Log files**: The actual logs are stored in the `/var/log` directory.

**Facilities**: Indicate the source of the message. There are 24 different syslog facilities that can be described below:

| **Numerical Code** | **Keyword** | **Facility Name** |
| --- | --- | --- |
| 0 | kern | Kernel messages |
| 1 | user | User-level messages |
| 2 | mail | Mail system |
| 3 | daemon | System daemons |
| 4 | auth | Security/authentication messages |
| 5 | syslog | Internal syslog messages |
| 6 | lpr | Line printer subsystem |
| 7 | news | Network news subsystem |
| 8 | uucp | UUCP subsystem |
| 9 | cron | Cron subsystems |
| 10 | authpriv | Security messages |
| 11 | ftp | FTP daemon |
| 12 | ntp | NTP subsystem |
| 13 | security | Security log audit |
| 14 | console | Console log alerts |
| 15 | solaris-cron | Scheduling logs |
| 16-23 | local0 to local7 | Locally used facilities |
