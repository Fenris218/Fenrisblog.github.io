---
title: "Authenticate"
date: 2025-09-16 14:18:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "What if the user enters the wrong password or the authentication fails for any other reason?"
media_subpath: /assets/img/tryhackme/2025-09-16-authenticate/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/monitoring-active-directory/authenticate/
th_id: "soc-lv-2/active-directory/monitoring-active-directory/authenticate"
th_parent: "soc-lv-2/active-directory/monitoring-active-directory"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/monitoring-active-directory"]
---

{% include tryhackme-nav.html %}

![image.png](image.png)

![image.png](image%201.png)

**What if the user enters the wrong password or the authentication fails for any other reason?**

The pre-authentication step fails, generating Event 4771 on the Domain Controller. We'll see 4771 events regularly in environments where users sometimes forget or mistype their passwords.

**Encryption Types in 4768/4769**

Tickets usually are encrypted, and AD uses two encryption types for this:

- **RC4** encryption appears in environments with older systems or applications that don't support AES.
- And **AES-256** encryption, which modern systems use.

Understanding what should usually appear in our environment helps us determine which encryption types to expect and where they come from.

| **Value** | **Algorithm** | **When You See It** |
| --- | --- | --- |
| 0x12 | AES-256 | Modern systems, Windows 2008+ domain functional level |
| 0x17 | RC4-HMAC | Legacy systems, older applications, cross-forest trusts |

Let's say we want to filter for TGT requests in Splunk. We can use the following query:

```sql
index=* EventCode=4768
| table _time, Account_Name, Client_Address, Ticket_Encryption_Type
| --- |
```

![image.png](image%202.png)
