---
title: "Kernel Logs"
date: 2025-07-31 15:31:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Logs Investigations"]
tags: ["tryhackme", "linux-logs-investigations"]
description: "We can view the current contents of the ring buffer by running the command dmesg"
media_subpath: /assets/img/tryhackme/2025-07-31-kernel-logs/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-logs-investigations/kernel-logs/
th_id: "soc-lv1/linux-logs-investigations/kernel-logs"
th_parent: "soc-lv1/linux-logs-investigations"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/linux-logs-investigations"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-logs-investigations"]
---

{% include tryhackme-nav.html %}

We can view the current contents of the ring buffer by running the command `dmesg`

```bash
ubuntu@tryhackme:~$ sudo dmesg
[    0.000000] Linux version 5.15.0-1063-aws (buildd@lcy02-amd64-003) (gcc (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #69~20.04.1-Ubuntu SMP Fri May 10 19:20:12 UTC 2024 (Ubuntu 5.15.0-1063.69~20.04.1-aws 5.15.152)
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-5.15.0-1063-aws root=PARTUUID=da63a61e-01 ro console=tty1 console=ttyS0 nvme_core.io_timeout=4294967295 panic=-1
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000]   Hygon HygonGenuine
```

kernel logs are stored in the `/var/log/kern.log`
