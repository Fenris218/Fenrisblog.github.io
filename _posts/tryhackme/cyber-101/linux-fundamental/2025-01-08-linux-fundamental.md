---
title: "Linux fundamental"
date: 2025-01-08 15:07:00 +0700
categories: ["TryHackMe", "Cyber 101", "Linux fundamental"]
tags: ["tryhackme", "linux-fundamental"]
description: ""
media_subpath: /assets/img/tryhackme/2025-01-08-linux-fundamental/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/linux-fundamental/
th_id: "cyber-101/linux-fundamental"
th_parent: "cyber-101"
th_kind: module
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/linux-fundamental"
th_size: 1
th_ancestors: ["cyber-101"]
---

{% include tryhackme-nav.html %}

- /etc/sudoers :  contains a list of the users & groups that have permission to run sudo or a set of commands as the root user.
- /tmp :  directory is volatile and is used to store data that is only needed to be accessed once or twice. ⇒  useful for pentester is that any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.
- /var : This folder stores data that is frequently accessed or written by services or applications running on the system. For example, log files from running services and applications are written here
- Transfer file from Host-SCP (SSH ) :

```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

- Make your computer become a server :

```bash
python3 -m http.server
```

- **How do Processes Start?:** systemd là tiến trình gốc (PID 1) của Ubuntu, chịu trách nhiệm quản lý toàn bộ tiến trình trong hệ thống, hoạt động như “cầu nối” giữa nhân Linux và người dùng. Bất kỳ chương trình hay phần mềm nào mà ta muốn khởi động sau đó đều sẽ được tạo ra dưới dạng “tiến trình con (child process)” của systemd. ⇒ Điều này có nghĩa là các tiến trình đó được **systemd quản lý**, nhưng vẫn **chạy độc lập như một tiến trình riêng** (mặc dù **chia sẻ tài nguyên** với systemd), giúp cho việc **nhận diện, giám sát, và quản lý** chúng dễ dàng hơn.
- **Getting Processes/Services to Start on Boot :** `systemctl` -- this command allows us to interact with the **systemd** process/daemon.
    
    ```bash
    systemctl [option] [service]
    ```
    
- Dung toan tu & sau lệnh để đưa nó vào chế độ background
- **cron** :là một **daemon (process chạy nền)** dùng để **lên lịch thực thi các tác vụ (jobs) theo thời gian định sẵn**. Nó thường được dùng để tự động hóa các nhiệm vụ lặp lại như backup, gửi email, cập nhật hệ thống, hoặc chạy script. **crontab** là file cấu hình cho cron

