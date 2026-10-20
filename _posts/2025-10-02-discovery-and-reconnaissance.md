---
title: "Discovery and Reconnaissance"
date: 2025-10-02 18:34:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "AD discovery is what gives attackers the map they need to plan their lateral movement."
media_subpath: /assets/img/tryhackme/2025-10-02-discovery-and-reconnaissance/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-lateral-movement/discovery-and-reconnaissance/
th_id: "soc-lv-2/active-directory/detecting-ad-lateral-movement/discovery-and-reconnaissance"
th_parent: "soc-lv-2/active-directory/detecting-ad-lateral-movement"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-lateral-movement"]
---

{% include tryhackme-nav.html %}

AD discovery is what gives attackers the map they need to plan their lateral movement.

Let's look at some Active Directory discovery commands commonly used in real-world attacks. The table below lists the commands you'll encounter most often:

| **Category** | **Command** | **What It Reveals** |
| --- | --- | --- |
| Domain/Trust | nltest /dclist:domain | Domain controllers in the environment |
| Domain/Trust | nltest /domain_trusts | Trusted domains the attacker could pivot to |
| Accounts/Groups | net user /domain | All domain user accounts |
| Accounts/Groups | net group "Domain Admins" /domain | Members of the Domain Admins group |
| Accounts/Groups | net group "Enterprise Admins" /domain | Members of the Enterprise Admins group |
| Accounts/Groups | net localgroup administrators | Local admin accounts on the current machine |
| Systems | net view | Machines visible on the network |
| Systems | net view \THM-SHR-SRV /all | Shares on a specific remote system |
| PowerShell | Get-ADUser -Filter * | AD user enumeration via PowerShell |
| PowerShell | Get-ADGroupMember "Domain Admins" | Admin group members via PowerShell |
| PowerShell | Get-ADComputer -Filter * | All computer accounts in the domain |

None of these commands requires admin privileges. Active Directory grants read access to all authenticated domain users by default. This is by design, not a misconfiguration, and it's one of the reasons lateral movement planning might sometimes be easy for attackers.

Also, attackers use third-party tools like `adfind.exe` (heavily used by ransomware groups like Conti and FIN7), `dsquery`, and PowerShell's `[System.DirectoryServices.DirectorySearcher]` class for raw LDAP queries.

**Detecting Discovery With Sysmon and PowerShell Logs**

We detect these commands through two log sources:

- Sysmon Event 1 captures process creation, where the CMD/PowerShell commands appear in the command line.
- PowerShell Event 4104 captures Script Block Logging, which records the PowerShell commands and cmdlets executed.
