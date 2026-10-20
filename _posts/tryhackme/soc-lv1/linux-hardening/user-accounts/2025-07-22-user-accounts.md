---
title: "User Accounts"
date: 2025-07-22 18:22:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Hardening"]
tags: ["tryhackme", "linux-hardening"]
description: ""
media_subpath: /assets/img/tryhackme/2025-07-22-user-accounts/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-hardening/user-accounts/
th_id: "soc-lv1/linux-hardening/user-accounts"
th_parent: "soc-lv1/linux-hardening"
th_kind: note
th_order: 4
th_course: "soc-lv1"
th_module: "soc-lv1/linux-hardening"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-hardening"]
---

{% include tryhackme-nav.html %}

- Sử dụng Sudo ( thêm vào group sudo/wheel)
- Disable root : Once you have created an account for administrative purposes and added it to the `sudo`/`wheel` group, you might consider disabling the `root` account. A straightforward way is to modify the `/etc/passwd` and change the `root` shell to `/sbin/nologin`. In other words, edit `/etc/passwd` and change the line `root:x:0:0:root:/root:/bin/bash` to `root:x:0:0:root:/root:/sbin/nologin`.
- Enforce a Strong Password Policy
- Disable Unused Accounts :  An easy way would be to edit the `/etc/passwd` file and set the shell of the user account we want to disable to `/sbin/nologin`. We should do the same for local services.
