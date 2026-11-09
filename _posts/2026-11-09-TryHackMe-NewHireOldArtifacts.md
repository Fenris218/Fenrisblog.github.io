---
title: TryHackMe-NewHireOldArtifacts
date: 2026-11-09 23:54:00 +0700
categories: [TryHackMe, Lab]
tags: [splunk, sysmon, windows-defender, powershell, wmic, registry, malware, nirsoft] # TAG names should always be lowercase
media_subpath: /assets/img/2026-11-09-TryHackMe_NewHireOldArtifacts/
toc: true
comments: false
---

![image.png](image.png)![image 1.png](image%201.png)

## 1. A Web Browser Password Viewer executed on the infected machine. What is the name of the binary? Enter the full path.
![image 2.png](image%202.png)
-> Answer : C:\Users\FINANC~1\AppData\Local\Temp\11111.exe

## 2. What is listed as the company name?
![image 3.png](image%203.png)
-> Answer : NirSoft

## 3. Another suspicious binary running from the same folder was executed on the workstation. What was the name of the binary? What is listed as its original filename? (**format: file.xyz,file.xyz**)
![image 4.png](image%204.png)
-> Answer : PalitExplorer.exe,IonicLarge.exe

## 4. The binary from the previous question made two outbound connections to a malicious IP address. What was the IP address? Enter the answer in a defang format.
![image 5.png](image%205.png)
-> Answer : 2[.]56[.]59[.]42

## 5. The same binary made some change to a registry key. What was the key path?
![image 6.png](image%206.png)
-> Answer : HKLM\SOFTWARE\Policies\Microsoft\Windows Defender

## 6. Some processes were killed and the associated binaries were deleted. What were the names of the two binaries? (**format: file.xyz,file.xyz**)

Query : index=* taskkill /im
![image 7.png](image%207.png)
-> Answer : phcIAmLJMAIMSa9j9MpgJo1m.exe, WvmIOrcfsuILdX6SNwIRmGOJ.exe

## 7. The attacker ran several commands within a PowerShell session to change the behaviour of Windows Defender. What was the last command executed in the series of similar commands?
WMIC (Windows Management Instrumentation Command-line)
![image 8.png](image%208.png)
-> Answer : powershell WMIC /NAMESPACE:\\root\Microsoft\Windows\Defender PATH MSFT_MpPreference call Add ThreatIDDefaultAction_Ids=2147735503 ThreatIDDefaultAction_Actions=6 Force=True

## 8. Based on the previous answer, what were the four IDs set by the attacker? Enter the answer in order of execution. (format: 1st,2nd,3rd,4th)
![image 9.png](image%209.png)
-> Answer : 2147735503,2147737010,2147737007,2147737394

## 9. Another malicious binary was executed on the infected workstation from another AppData location. What was the full path to the binary?
![image 10.png](image%2010.png)
-> Answer : C:\Users\Finance01\AppData\Roaming\EasyCalc\EasyCalc.exe

## 10. What were the DLLs that were loaded from the binary from the previous question? Enter the answers in alphabetical order. (format: file1.dll,file2.dll,file3.dll)
![image 11.png](image%2011.png)
-> Answer : nw_elf.dll,ffmpeg.dll,nw.dll