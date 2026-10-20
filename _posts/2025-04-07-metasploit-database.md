---
title: "Metasploit Database"
date: 2025-04-07 08:36:00 +0700
categories: ["TryHackMe", "Cyber 101", "Metasploit"]
tags: ["tryhackme", "metasploit"]
description: "https://tryhackme.com/room/metasploitexploitation?taskNo=3&sharerId=6704a924d9503f79da2f5690"
media_subpath: /assets/img/tryhackme/2025-04-07-metasploit-database/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/metasploit/metasploit-exploitation/metasploit-database/
th_id: "cyber-101/metasploit/metasploit-exploitation/metasploit-database"
th_parent: "cyber-101/metasploit/metasploit-exploitation"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/metasploit"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/metasploit", "cyber-101/metasploit/metasploit-exploitation"]
---

{% include tryhackme-nav.html %}

https://tryhackme.com/room/metasploitexploitation?taskNo=3&sharerId=6704a924d9503f79da2f5690

Metasploit Database using the `msfdb init` command

Check the database status using the `db_status` command.

You can list available workspaces using the `workspace` command.

![image.png](image.png)

If you run a Nmap scan using the `db_nmap` shown below, all results will be saved to the database.

![image.png](image%201.png)

You can now reach information relevant to hosts and services running on target systems with the `hosts` and `services` commands, respectively. 

![image.png](image%202.png)
