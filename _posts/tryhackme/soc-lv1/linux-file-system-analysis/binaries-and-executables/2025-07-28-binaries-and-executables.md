---
title: "Binaries and Executables"
date: 2025-07-28 12:28:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux File System Analysis"]
tags: ["tryhackme", "linux-file-system-analysis"]
description: "SetUID (SUID) and SetGID (SGID) are special permission bits in Unix operating systems. These permission bits change the behaviour of executable files, allowi…"
media_subpath: /assets/img/tryhackme/2025-07-28-binaries-and-executables/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-file-system-analysis/binaries-and-executables/
th_id: "soc-lv1/linux-file-system-analysis/binaries-and-executables"
th_parent: "soc-lv1/linux-file-system-analysis"
th_kind: note
th_order: 4
th_course: "soc-lv1"
th_module: "soc-lv1/linux-file-system-analysis"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-file-system-analysis"]
---

{% include tryhackme-nav.html %}

## Binaries permissions

SetUID (SUID) and SetGID (SGID) are special permission bits in Unix operating systems. These permission bits change the behaviour of executable files, allowing them to run with the privileges of the file owner or group rather than the privileges of the user who executes the file.

→ If a binary or executable on the system is misconfigured with an SUID or SGID permission set, an attacker may abuse the binary to break out of a restricted (unprivileged) shell through legitimate but unintended use of that binary. For example, if the PHP binary contained a SUID bit to run as root, it's trivial for an attacker to abuse it to run system commands through PHP's system exec functions as root.

```bash
investigator@10.49.157.181:~$ find / -perm -u=s -type f 2>/dev/null
...
/usr/bin/fusermount
/usr/bin/python3.8
/usr/bin/at
/usr/bin/mount
/var/tmp/bash
/mnt/usb/lib/dbus-1.0/dbus-daemon-launch-helper
...
```

`-u=s` : có bật SUID : chạy với quyền owner của file

`-g=s` : có bật SGID : chạy với quyền group của file

Một vài ví dụ risk điển hình : 

- Python should never be given SUID permission, as it is trivial to escalate privileges to the owner.
- UID binaries in the `/tmp` or `/var/tmp` directory stand out as these directories are typically writable by all users, and unauthorised creation of SUID binaries in these directories poses a notable risk.

```bash
investigator@10.49.157.181:~$ sudo cat /home/jane/.bash_history | grep -B 2 -A 2 "python"
ls -al
find / -perm -u=s -type f 2>/dev/null
/usr/bin/python3.8 -c 'import os; os.execl("/bin/sh", "sh", "-p", "-c", "cp /bin/bash /var/tmp/bash && chown root:root /var/tmp/bash && chmod +s /var/tmp/bash")'
ls -al /var/tmp
/var/tmp/bash -p
exit
```

From the output, we've discovered evidence of Jane's user account identifying SUID binaries with the `find` command and abusing the SUID permission on the Python binary to run system commands as the root user. With this level of command execution, the attacker was able to create a copy of the `/bin/bash` binary (the Bash shell executable) and place it into the `/var/tmp` folder. Additionally, the attacker changed the owner of this file to root and added the SUID permission to it (`chmod +s`).

## Kiểm tra tính nguyên vẹn của các package được tải

`debsums`  : is a command-line utility for Debian-based Linux systems that verifies the integrity of installed package files.

```bash
investigator@10.49.157.181:~$ sudo debsums -e -s
debsums: changed file /***/******* (from sudo package)
```
