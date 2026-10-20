---
title: "Asset & indentifies"
date: 2025-06-08 10:38:00 +0700
categories: ["TryHackMe", "SOC LV1", "SOC Workbooks and Lookups"]
tags: ["tryhackme", "soc-workbooks-and-lookups"]
description: "Identity Inventory"
media_subpath: /assets/img/tryhackme/2025-06-08-asset-indentifies/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/soc-workbooks-and-lookups/asset-indentifies/
th_id: "soc-lv1/soc-workbooks-and-lookups/asset-indentifies"
th_parent: "soc-lv1/soc-workbooks-and-lookups"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/soc-workbooks-and-lookups"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/soc-workbooks-and-lookups"]
---

{% include tryhackme-nav.html %}

**Identity Inventory**

Identity inventory is a catalogue of corporate employees (user accounts), services (machine accounts), and their details like privileges, contacts, and roles within the company. For the scenario above, identity inventory would help you get context about G.Baker and R.Lund, and make it simpler to decide if the activity was expected or not.

- **Example of Identities**
    
    
    | **Full Name** | **Username** | **Email** | **Role** | **Location** | **Access** |
    | --- | --- | --- | --- | --- | --- |
    | Gregory Baker | G.Baker | g.baker@tryhatme.thm | Chief Financial Officer | Europe, UK | VPN, HQ, FINANCE |
    | Raymond Lund | R.Lund | r.lund@tryhatme.thm | US Financial Adviser | US, Texas | VPN, FINANCE |
    | Kate Danner | K.Danner | k.danner@tryhatme.thm | Chief Technology Officer | Europe, UK | VPN, DA, HQ, AWS |
    | svc-veeam-06 | svc-veeam-06 | N/A | Backup Service Account | N/A | VEEAM, DMZ, HQ |
    | svc-nginx-pp | svc-nginx-pp | N/A | Web App Service Account | N/A | DMZ |

**Sources of Identities**

| **Solution** | **Examples** | **Description** |
| --- | --- | --- |
| Active Directory | On-prem AD, Entra ID | AD itself is an identity database, and it is commonly used by SOC |
| SSO Providers | Okta, Google Workspace | Cloud alternative for AD, an easy way to manage and search the users |
| HR Systems | BambooHR, SAP, HiBob | Limited to employees only, but usually provides full employee data |
| Custom Solution | CSV or Excel Sheets | It is common for IT or security teams to maintain their own solutions |

**Asset Inventory**

Asset inventory, also called asset lookup, is a list of all computing resources within an organisation's IT environment. Note that while "asset" is a vague term and can also refer to software, hardware, or employees

- **Example of Assets**
    
    
    | **Hostname** | **Location** | **IP Address** | **OS** | **Owner** | **Purpose** |
    | --- | --- | --- | --- | --- | --- |
    | HQ-FINFS-02 | UK Datacenter | 172.16.15.89 | Windows Server 2022 | Central IT | File server for financial records |
    | HQ-ADDC-01 | UK Datacenter | 172.16.15.10 | Windows Server 2019 | Central IT | Primary AD domain controller |
    | PC-891D | London Office | 192.168.5.13 | Windows 11 Pro | Tech Support | Stationary PC for accountants |
    | L007694 | Remote | N/A | MacOS 13 | A.Kelly, DevOps | Corporate laptop |
    | L005325 | Remote | N/A | MacOS 13 | J.Eldridge, HR | Corporate laptop |

**Sources of Assets**

| **Solution** | **Examples** | **Description** |
| --- | --- | --- |
| Active Directory | On-prem AD, Entra ID | AD is not only an identity but also a solid asset inventory database |
| SIEM or EDR | Elastic, CrowdStrike | Some SIEM or EDR agents collect information about the monitored hosts |
| MDM Solution | MS Intune, Jamf MDM | A dedicated class of solutions created to list and manage assets |
| Custom Solution | CSV or Excel Sheets | Same as with the identity inventory, custom solutions are common |
