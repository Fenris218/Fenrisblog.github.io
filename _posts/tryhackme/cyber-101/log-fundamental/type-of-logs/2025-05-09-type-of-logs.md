---
title: "Type of Logs"
date: 2025-05-09 16:08:00 +0700
categories: ["TryHackMe", "Cyber 101", "Log Fundamental"]
tags: ["tryhackme", "log-fundamental"]
description: ""
media_subpath: /assets/img/tryhackme/2025-05-09-type-of-logs/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/log-fundamental/type-of-logs/
th_id: "cyber-101/log-fundamental/type-of-logs"
th_parent: "cyber-101/log-fundamental"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/log-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/log-fundamental"]
---

{% include tryhackme-nav.html %}

| **Log Type** | **Usage** | **Example** |
| --- | --- | --- |
| System Logs | The system logs can be helpful in troubleshooting running issues in the OS. These logs provide information on various operating system activities. | - System Startup and shutdown events- Driver Loading events- System Error events- Hardware events |
| Security Logs | The security logs help detect and investigate incidents. These logs provide information on the security-related activities in the system. | -Authentication events- Authorization events- Security Policy changes events- User Account changes events - Abnormal Activity events |
| Application Logs | The application logs contain specific events related to the application. Any interactive or non-interactive activity happening inside the application will be logged here. | - User Interaction events- Application Changes events- Application Update events- Application Error events |
| Audit Logs | The Audit logs provide detailed information on the system changes and user events. These logs are helpful for compliance requirements and can play a vital role in security monitoring as well. | - Data Access events- System Change events- User Activity events- Policy Enforcement events |
| Network Logs | Network logs provide information on the network’s outgoing and incoming traffic. They play crucial roles in troubleshooting network issues and can also be handy during incident investigations. | - Incoming Network Traffic events- Outgoing Network Traffic events- Network Connection Logs - Network Firewall Logs |
| Access Logs | The Access logs provide detailed information about the access to different resources. These resources can be of different types, providing us with information on their access. | - Webserver Access Logs- Database Access Logs - Application Access Logs- API Access Logs |
