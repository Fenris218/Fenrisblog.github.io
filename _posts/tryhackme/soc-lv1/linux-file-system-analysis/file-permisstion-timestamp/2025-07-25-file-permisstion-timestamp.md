---
title: "File,Permisstion,Timestamp"
date: 2025-07-25 09:25:00 +0700
categories: ["TryHackMe", "SOC LV1", "Linux File System Analysis"]
tags: ["tryhackme", "linux-file-system-analysis"]
description: "Attackers often target directories with write permissions to upload malicious files. Common writable directories include:"
media_subpath: /assets/img/tryhackme/2025-07-25-file-permisstion-timestamp/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/linux-file-system-analysis/file-permisstion-timestamp/
th_id: "soc-lv1/linux-file-system-analysis/file-permisstion-timestamp"
th_parent: "soc-lv1/linux-file-system-analysis"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/linux-file-system-analysis"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/linux-file-system-analysis"]
---

{% include tryhackme-nav.html %}

## Ownership and Permissions

Attackers often target directories with write permissions to upload malicious files. Common writable directories include:

- **/tmp**: The temporary directory is writable by all users, making it a common choice.
- **/var/tmp**: Another temporary directory commonly with world write permissions.
- **/dev/shm**: The shared memory file system, which is also normally writable by all users.

 We can also leverage the `find` command to quickly identify files that match our criteria. For example:

```bash
investigator@10.49.140.208:~$ find / -user www-data -type f 2>/dev/null | less
/var/www/html/assets/reverse.elf
/var/www/html/uploads/MzCxVeR.jpeg
/var/www/html/uploads/AzSxWqE.jpeg
/var/www/html/uploads/QaWsEdR.jpeg
/var/www/html/uploads/TyHjKlM.jpeg
```

| `find / -group GROUPNAME 2>/dev/null` | Retrieve a list of files and directories owned by a specific group. |
| --- | --- |
| `find / -perm -o+w 2>/dev/null` | Retrieve a list of all world-writable files and directories. |
| `find / -type f -cmin -5 2>/dev/null` | Retrieve a list of files created or changed within the last five minutes. |

### Timestamp

- **Modify Timestamp (mtime):** This timestamp reflects the last time the **contents** of a file were modified or altered. Whenever a file is written to or changed, its *mtime* is updated.
- **Change Timestamp (ctime):** This timestamp indicates the last time a file's **metadata** was changed. Metadata includes attributes like permissions, ownership, or the filename itself. Whenever any metadata associated with a file changes, its *ctime* is updated.
- **Access Timestamp (atime):** This timestamp indicates the last time a file was **accessed** or read. Whenever a file is opened, its *atime* is updated.

![image.png](image.png)
