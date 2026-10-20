---
title: "Filesystem Partitioning and Encryption"
date: 2025-07-18 14:18:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux Hardening"]
tags: ["tryhackme", "linux-hardening"]
description: "In the scenario where an adversary has complete physical access to your laptop, for instance, by stealing it, we want to ensure that it won’t be of any use t…"
media_subpath: /assets/img/tryhackme/2025-07-18-filesystem-partitioning-and-encryption/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-hardening/filesystem-partitioning-and-encryption/
th_id: "soc-lv1/linux-hardening/filesystem-partitioning-and-encryption"
th_parent: "soc-lv1/linux-hardening"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/linux-hardening"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-hardening"]
---

{% include tryhackme-nav.html %}

In the scenario where an adversary has complete physical access to your laptop, for instance, by stealing it, we want to ensure that it won’t be of any use to them. A disk drive full of encrypted data should be as good as a damaged one.

There are various software systems and tools that provide encryption to Linux systems. Since many modern Linux distributions ship with LUKS (Linux Unified Key Setup), let’s cover it in more detail.

## LUKS : https://tryhackme.com/room/linuxsystemhardening

LUKS dùng để mã hóa ổ đĩa, cho nên để có thể đọc thì cần LUKSOPEN trước ( cần mật khẩu ) , sau đó mới mount để đọc

```bash
tryhackme@ip-10-48-155-215:~$ file /home/tryhackme/secretvault.img
/home/tryhackme/secretvault.img: LUKS encrypted file, ver 1 [aes, xts-plain64, sha256] UUID: 45cb6108-aac0-44cb-83f6-59f7b9754a16
tryhackme@ip-10-48-155-215:~$ sudo cryptsetup luksOpen  /home/tryhackme/secretvault.img vault
Enter passphrase for /home/tryhackme/secretvault.img:
tryhackme@ip-10-48-155-215:~$ sudo cryptsetup -v status vault
/dev/mapper/vault is active.
  type:    LUKS1
  cipher:  aes-xts-plain64
  keysize: 512 bits
  key location: dm-crypt
  device:  /dev/loop8
  loop:    /home/tryhackme/secretvault.img
  sector size:  512
  offset:  4096 sectors
  size:    1044480 sectors
  mode:    read/write
Command successful.
tryhackme@ip-10-48-155-215:~$ ls -l /dev/mapper/vault
lrwxrwxrwx 1 root root 7 Apr  1 08:12 /dev/mapper/vault -> ../dm-0
tryhackme@ip-10-48-155-215:~$ mkdir VAULT
tryhackme@ip-10-48-155-215:~$ sudo mount /dev/mapper/vault VAULT
tryhackme@ip-10-48-155-215:~$ cd VAULT
tryhackme@ip-10-48-155-215:~/VAULT$ ls
lost+found  task3_flag.txt
tryhackme@ip-10-48-155-215:~/VAULT$ cat task3_flag.txt
THM{LUKS_not_LUX}
```
