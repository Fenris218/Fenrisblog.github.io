---
title: "Runtime Monitoring"
date: 2025-07-15 11:15:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logging for SOC"]
tags: ["tryhackme", "linux-logging-for-soc"]
description: "By default, Linux does not comprehensively log runtime events such as process execution, file access, or network syscalls at the syscall level. The Audit fra…"
media_subpath: /assets/img/tryhackme/2025-07-15-runtime-monitoring/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logging-for-soc/runtime-monitoring/
th_id: "soc-lv1/linux-logging-for-soc/runtime-monitoring"
th_parent: "soc-lv1/linux-logging-for-soc"
th_kind: note
th_order: 3
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logging-for-soc"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logging-for-soc"]
---

{% include tryhackme-nav.html %}

By default, Linux does not comprehensively log runtime events such as process execution, file access, or network syscalls at the syscall level. The Audit framework (`auditd`) fills this gap.

## Core OS concept

![image.png](image.png)

Why do you need to know about system calls? Well, all modern EDRs and logging tools rely on them - they monitor the main system calls and log the details in a human-readable format. Since there is nearly no way for attackers to bypass system calls, all you have to do is choose the system calls you'd like to log and monitor. In the next task, you will try it in practice using auditd.
