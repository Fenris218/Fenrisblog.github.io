---
title: TryHackMe-IronShade
date: 2026-10-06 09:11:00 +0700
categories: [CTF, Forensic, Linux, TryHackMe]
tags: [forensic, linux, compromise-assessment, persistence, cronjob, systemd, authlog, dpkg] # TAG names should always be lowercase
media_subpath: /assets/img/2026-10-06-TryHackMe_IronShade/
toc: true
comments: false
---

## Incident Scenario  

Based on the threat intel report received, an infamous hacking group, **IronShade**, has been observed targeting Linux servers across the region. Our team had set up a honeypot and exposed weak SSH and ports to get attacked by the APT group and understand their attack patterns. 

You are provided with one of the compromised Linux servers. Your task as a Security Analyst is to perform a thorough compromise assessment on the Linux server and identify the attack footprints. Some threat reports indicate that one indicator of their attack is creating a backdoor account for persistence.

### What is the Machine ID of the machine we are investigating?
![image.png](image.png)
-> Answer : dc7c8ac5c09a4bbfaf3d09d399f10d96

### What backdoor user account was created on the server?
```
cut -d : -f1 /etc/passwd
```
![image 1.png](image%201.png)
-> Answer : mircoservice

### What is the cronjob that was set up by the attacker for persistence?
```
sudo cat /var/spool/cron/crontabs/root
```
![image 2.png](image%202.png)
-> Answer : /home/mircoservice/printer_app

### Examine the running processes on the machine. Can you identify the suspicious-looking hidden process from the backdoor account?
```
ps aux | grep mirco
```
![image 3.png](image%203.png)
-> Answer : .stroke

### How many processes are found to be running from the backdoor account’s directory?
-> Answer : 2

### What is the name of the hidden file in memory from the root directory?
```
ls -la /
```
![image 4.png](image%204.png)
-> Answer : .systmd

### What suspicious services were installed on the server? Format is service a, service b in alphabetical order.
```
sudo find /etc/systemd/system /lib/systemd/system /usr/lib/systemd/system \
-type f -name "*.service" -printf '%TY-%Tm-%Td %TH:%TM:%TS %p\n' 2>/dev/null | sort -r | head -n 5
```
![image 5.png](image%205.png)
-> Answer : backup.service, strokes.service

### Examine the logs; when was the backdoor account created on this infected system?
```
grep -aEi "useradd|adduser" /var/log/auth.log
```
![image 6.png](image%206.png)
-> Answer : Aug 5 22:05:33

### From which IP address were multiple SSH connections observed against the suspicious backdoor account?
```
grep -a ssh /var/log/auth.log* | grep -i mircoservice
```
![image 7.png](image%207.png)
-> Answer : 10.11.75.247 

### Which malicious package was installed on the host?
```
cat /var/log/dpkg.log | grep install
```
![image 8.png](image%208.png)
-> Answer : pscanner

### What is the secret code found in the metadata of the suspicious package?
```
dpkg -s pscanner
```
![image 9.png](image%209.png)
-> Answer : {_tRy_Hack_ME_}