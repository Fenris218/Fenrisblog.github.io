---
title: "Account, Groups and Resource Access Events"
date: 2025-09-17 15:19:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "Account Lifecycle Events"
media_subpath: /assets/img/tryhackme/2025-09-17-account-groups-and-resource-access-events/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/monitoring-active-directory/account-groups-and-resource-access-events/
th_id: "soc-lv-2/active-directory/monitoring-active-directory/account-groups-and-resource-access-events"
th_parent: "soc-lv-2/active-directory/monitoring-active-directory"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/monitoring-active-directory"]
---

{% include tryhackme-nav.html %}

**Account Lifecycle Events**

| **Event ID** | **What Happened** |
| --- | --- |
| 4720 | Account created |
| 4722 | Account enabled |
| 4724 | Password reset attempted |
| 4725 | Account disabled |
| 4740 | Account locked out |

**Group Membership Events**

| **Event ID** | **What Happened** | **Group Scope** |
| --- | --- | --- |
| 4728 | Member added to the global security group | Domain-wide |
| 4732 | Member added to local security group | Machine-level (domain local on DCs) |
| 4756 | Member added to universal security group | Entire forest |

**Directory Service Events**

Event 5136 logs attribute-level modifications to Active Directory objects. Unlike Event 4728, which only indicates that someone was added to a group, Event 5136 shows the specific LDAP attribute that changed and its new value.

These are the attributes we'll see most often:

- `userAccountControl` - Account status changes (disabled, password never expires, etc.)
- `servicePrincipalName` - SPN modifications
- `scriptPath` - Logon script path (scripts that run when users log in)
- `member` - Group membership modifications at the attribute level
- `displayName`, `description`, `title` - User information fields

**Tracking GPO Modifications**

One important use case for Event 5136 is monitoring changes to Group Policy Objects. GPOs allow administrators to manage configuration across the domain centrally. A single GPO can deploy software, configure security settings, or change audit policies on thousands of machines at once.

**Common Service Name Patterns**

| **ServiceName Pattern** | **What It Represents** |
| --- | --- |
| krbtgt | TGT renewal requests |
| cifs/THM-SHR-SRV | File share access |
| ldap/THM-DC | Directory queries |
| http/THM-WEB-SRV | Web application access |
| MSSQLSvc/THM-SQL-SRV | SQL Server access |
| HOST/THM-IT-DESK | General host services |

**Service Account Patterns**

| **Account Type** | **Expected Pattern** |
| --- | --- |
| SQL service accounts | Access database servers from application servers |
| Backup service accounts | Access file shares from backup servers, typically overnight |
| Monitoring accounts | Query multiple systems at regular intervals |
| Admin accounts | Access from designated admin workstations during business hours |
