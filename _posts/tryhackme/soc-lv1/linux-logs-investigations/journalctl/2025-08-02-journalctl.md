---
title: "Journalctl"
date: 2025-08-02 17:33:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logs Investigations"]
tags: ["tryhackme", "linux-logs-investigations"]
description: "The journal and journalctl tools provide a powerful logging system for modern Linux distributions, capturing log messages from the kernel, system services, a…"
media_subpath: /assets/img/tryhackme/2025-08-02-journalctl/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logs-investigations/journalctl/
th_id: "soc-lv1/linux-logs-investigations/journalctl"
th_parent: "soc-lv1/linux-logs-investigations"
th_kind: note
th_order: 3
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logs-investigations"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logs-investigations"]
---

{% include tryhackme-nav.html %}

The `journal` and `journalctl` tools provide a powerful logging system for modern Linux distributions, capturing log messages from the kernel, system services, and user applications.
(có thể query log)

### **Understanding the Journal**

The `journal` is a binary logging system used by systemd-based distributions. Unlike traditional text-based log files, the journal provides structured, indexed logs, allowing for efficient querying and filtering. This makes it easier to search and analyse logs, especially for security investigations.

Typically, journal logs are volatile and would be erased on the next system restart. This can be changed within its configuration file `/etc/systemd/journald.conf` by setting the **Storage** parameter to **persistent** and restarting the systemd journal daemon for the setting to take effect.
