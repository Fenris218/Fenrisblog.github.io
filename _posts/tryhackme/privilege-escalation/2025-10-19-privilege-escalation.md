---
title: "Privilege Escalation"
date: 2025-10-19 11:51:00 +0700
categories: ["TryHackMe", "Privilege Escalation"]
tags: ["tryhackme"]
description: "Để leo quyền đầu tiên cần hiểu về hệ thống hiện tại : OS, Network, User, File,.."
media_subpath: /assets/img/tryhackme/2025-10-19-privilege-escalation/
toc: true
comments: false
hidden: true
permalink: /tryhackme/privilege-escalation/
th_id: "privilege-escalation"
th_parent: "root"
th_kind: course
th_order: 4
th_course: "privilege-escalation"
th_module: ""
th_size: 0
th_ancestors: []
---

{% include tryhackme-nav.html %}

## 1. Enumeration

Để leo quyền đầu tiên cần hiểu về hệ thống hiện tại : OS, Network, User, File,..

### a. OS information

```

## List hostname and Kernel version
john@home:~$ uname -a
Linux home 6.8.0-41-generic

## xem phiên bản complier dùng build kernel và version kernel
cat /proc/version

## xem thông tin đối với OS đã được custom
cat /etc/issue 

## cron service
cat /etc/crontab
cat /var/spool/cron/
cat /etc/cron.d/

## list installed package
dpkg -l

```

### b. User

The `id` command : provide a general overview of the user’s privilege level and group memberships

```
john@home:~$ id
uid=1001(john) gid=1001(john) groups=1001(john),100(users)
john@home:~$ id matt
uid=1002(matt) gid=1002(matt) groups=1002(matt),27(sudo),116(admin)
```

`sudo -l`  : list all command user can run with sudo

`cat /etc/passwd` 

## 2. Basic privilege escalation

### a. Sudo

**sudo -l** 

```
john@sudo-box:~$ sudo -l
Matching Defaults entries for labuser on target:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin
User labuser may run the following commands on target:
    (ALL) NOPASSWD: /bin/cat
```

**Leverage Application Functions**

Ví dụ apache2 : has an option that supports loading alternative configuration files ( `-f`: specify an alternate ServerConfigFile).

⇒ Loading the `/etc/shadow` file using this option will result in an error message that includes the first line of the `/etc/shadow` file, but since that is the root line, it will basically give you the root hash, which can be cracked offline. On ubuntu the command is:

```
sudo apache2 -C "LoadModule mpm_event_module /usr/lib/apache2/modules/mod_mpm_event.so" -f /etc/shadow

```

**Leverage LD_PRELOAD**

On some systems, may see the LD_PRELOAD environment option.

```
john@sudo-box:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, **env_keep+=LD_PRELOAD**
User john may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
```

LD_PRELOAD is a function that allows any program to use shared libraries. If the "`env_keep`" option is enabled, you can generate a shared library that will be loaded and executed before the program is run. Please note that the LD_PRELOAD option will be ignored if the real user ID is different from the effective user ID.

The steps of this privilege escalation vector can be summarized as follows:

1. Check for LD_PRELOAD (with the env_keep option)
2. Write a simple C code compiled as a shared object (.so extension) file
3. Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file

### b. SUID

`find / -type f -perm -04000 -ls 2>/dev/null` will list files that have SUID or SGID bits set.
 GTFOBins ([https://gtfobins.github.io(opens in new tab)](https://gtfobins.github.io/)). 

### c. PATH
