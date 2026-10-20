---
title: "Users and Groups"
date: 2025-07-26 10:26:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux File System Analysis"]
tags: ["tryhackme", "linux-file-system-analysis"]
description: "Some important Linux groups that might be of interest to an attacker include:"
media_subpath: /assets/img/tryhackme/2025-07-26-users-and-groups/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-file-system-analysis/users-and-groups/
th_id: "soc-lv1/linux-file-system-analysis/users-and-groups"
th_parent: "soc-lv1/linux-file-system-analysis"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/linux-file-system-analysis"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-file-system-analysis"]
---

{% include tryhackme-nav.html %}

## **Identifying Groups**

Some important Linux groups that might be of interest to an attacker include:

- **sudo** or **wheel**: Members of the sudo (or wheel) group have the authority to execute commands with elevated privileges using sudo.
- **adm**: The adm group typically has read access to system log files.
- **shadow**: The shadow group is related to managing user authentication and password information. With this membership, a user can read the `/etc/shadow` file, which contains the password hashes of all users on the system.
- **disk**: Members of the disk group have almost unrestricted read and limited write access inside the system.

We can view all of the groups (and their respective group IDs) on the system by reading the `/etc/group` file

Trong `etc/sudoers` : là file cấu hình quyền `sudo`  cho các user/group

## User Logins and Activity

- last : It is used to display the history of the last logged-in users. It works by reading the `/var/log/wtmp` file
- lastb : tracks failed login attempts by reading the contents of `/var/log/btmp`, which can help identify login and password attacks.
- lastlog : Unlike the `last` command, which provides information about all user logins, the `lastlog` command focuses on a user's most recent login activity and reads from the `/var/log/lastlog` file.
- Failed Login Attempts : In addition to `lastb`, there are other ways to view failed login attempts on Linux through specific log files. The `/var/log/auth.log` file (or `/var/log/secure` on some distributions like CentOS or Red Hat) contains records of authentication-related events, including both successful and failed login attempts.
- UID =0 :  **quyền root tuyệt đối**
