---
title: "LSASS dumping"
date: 2025-09-27 13:29:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "LSASS holds different types of credentials depending on the Windows version and configuration:"
media_subpath: /assets/img/tryhackme/2025-09-27-lsass-dumping/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-credential-attacks/lsass-dumping/
th_id: "soc-lv-2/active-directory/detecting-ad-credential-attacks/lsass-dumping"
th_parent: "soc-lv-2/active-directory/detecting-ad-credential-attacks"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-credential-attacks"]
---

{% include tryhackme-nav.html %}

## **What LSASS Stores**

LSASS holds different types of credentials depending on the Windows version and configuration:

- NTLM password hashes for all authenticated users
- Kerberos tickets (TGTs and  tickets) for active sessions
    
    TGS
    
- Plaintext passwords on systems where WDigest is enabled (Windows 8/Server 2012 and earlier by default, or any newer version where the `UseLogonCredential` registry value has been set to `1`)
- Cached domain credentials for offline logon

## SYSMON event 10 ( Access process)

## **Understanding the GrantedAccess Field**

The `GrantedAccess` value is a hex bitmask built by adding together individual [process access rights(opens in new tab)](https://learn.microsoft.com/en-us/windows/win32/procthread/process-security-and-access-rights). Understanding how these values are composed helps when you encounter an unfamiliar access mask in the field:

| **Access Right** | **Hex Value** | **Purpose** |
| --- | --- | --- |
| PROCESS_QUERY_LIMITED_INFORMATION | 0x1000 | Query basic process info |
| PROCESS_QUERY_INFORMATION | 0x0400 | Query detailed process info |
| PROCESS_VM_READ | 0x0010 | Read process memory |
| PROCESS_ALL_ACCESS | 0x1FFFFF | Full access to the process |

For example, `0x1010` = `0x1000` (PROCESS_QUERY_LIMITED_INFORMATION) + `0x0010` (PROCESS_VM_READ). The `0x0010` bit is what matters for credential dumping, because reading LSASS process memory is how credentials are extracted.

In practice, `0x1010` is associated with Mimikatz, and `0x1FFFFF` (PROCESS_ALL_ACCESS) with ProcDump, comsvcs.dll, and Task Manager.

## **Understanding the CallTrace Field**

The `CallTrace` field shows the chain of DLL calls that led to the LSASS access, and it can distinguish between different dump methods:

- **Known DLLs** like `dbgcore.dll` and `dbghelp.dll` indicate the MiniDump API was used. This is how ProcDump and `comsvcs.dll` create memory dumps. It's a legitimate  being used for a malicious purpose.
    
    API
    
- **UNKNOWN memory offsets** (addresses not mapped to any known DLL) indicate injected code. This is the signature of Cobalt Strike beacons, Meterpreter, and other in-memory implants that access LSASS from injected shellcode.

To make this concrete, here's what each pattern looks like in a real CallTrace value:

**MiniDump-based (ProcDump/comsvcs.dll):**

```powershell
C:\Windows\SYSTEM32\ntdll.dll+9D4C4|C:\Windows\System32\KERNELBASE.dll+2B16D|C:\Windows\System32\dbgcore.dll+A3C8|...
```

**Injection-based (e.g., Cobalt Strike):**

```powershell
C:\Windows\SYSTEM32\ntdll.dll+9D4C4|UNKNOWN(0000025FA0120000)|UNKNOWN(0000025FA0124B30)|...
```

The diagram below provides a visual comparison of these two CallTrace patterns:

![image.png](image.png)
