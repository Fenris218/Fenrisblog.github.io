---
title: "Authentication Logs"
date: 2025-07-13 09:13:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logging for SOC"]
tags: ["tryhackme", "linux-logging-for-soc"]
description: "`/var/log/auth.log or /var/log/secure"
media_subpath: /assets/img/tryhackme/2025-07-13-authentication-logs/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logging-for-soc/authentication-logs/
th_id: "soc-lv1/linux-logging-for-soc/authentication-logs"
th_parent: "soc-lv1/linux-logging-for-soc"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logging-for-soc"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logging-for-soc"]
---

{% include tryhackme-nav.html %}

``/var/log/auth.log` or `/var/log/secure` 

![image.png](image.png)

## Login and Logout Events

 Each successful logon and logoff is logged, and you can see them by filtering the events containing the "session opened" or "session closed" keywords:

![image.png](image%201.png)

![image.png](image%202.png)

the SSH daemon stores its own log of successful and failed SSH logins. 

![image.png](image%203.png)

## Miscellaneous Events

You can also use the same log file to detect user management events. This is easy if you know basic Linux commands: If [useradd(opens in new tab)](https://www.man7.org/linux/man-pages/man8/useradd.8.html) is a command to add new users, just look for a "useradd" keyword to see user creation events! Below is an example of what you can see in the logs: password change, user deletion, and then privileged user creation.

![image.png](image%204.png)

In the example below, the "ubuntu" user used sudo to stop EDR, read firewall state, and finally access root via "sudo su":

![image.png](image%205.png)
