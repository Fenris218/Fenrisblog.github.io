---
title: "User Directories and Files"
date: 2025-07-27 11:27:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux File System Analysis"]
tags: ["tryhackme", "linux-file-system-analysis"]
description: ""
media_subpath: /assets/img/tryhackme/2025-07-27-user-directories-and-files/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-file-system-analysis/user-directories-and-files/
th_id: "soc-lv1/linux-file-system-analysis/user-directories-and-files"
th_parent: "soc-lv1/linux-file-system-analysis"
th_kind: note
th_order: 3
th_course: "soc-lv1"
th_module: "soc-lv1/linux-file-system-analysis"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-file-system-analysis"]
---

{% include tryhackme-nav.html %}

- We can list out the home directories with a simple `ls -l  /home`  command:

```bash
investigator@10.49.157.181:~$ ls -l /home
total 16
drwxr-xr-x 4 bob          bob          4096 Feb 12 19:32 bob
drwxr-xr-x 3 investigator investigator 4096 Feb 13 02:22 investigator
drwxr-xr-x 4 jane         jane         4096 Feb 13 00:36 jane
drwxr-xr-x 5 ubuntu       ubuntu       4096 Feb 12 21:23 ubuntu
```

- **.bashrc** and **.profile**: These are configuration files used to customise a user's Bash shell sessions and login environment, respectively.
- **.shh** : chứa cấu hình ssh cho 1 user
