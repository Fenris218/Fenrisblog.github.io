---
title: "Catagorize"
date: 2025-05-24 19:23:00 +0700
categories: ["TryHackMe", "Cyber 101", "Vulnerability Scanner Overview"]
tags: ["tryhackme", "vulnerability-scanner-overview"]
description: "Vulnerability scans can be categorized into many types; however, the major categorization of these scans are explained below: Authenticated vs. Unauthenticat…"
media_subpath: /assets/img/tryhackme/2025-05-24-catagorize/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/vulnerability-scanner-overview/catagorize/
th_id: "cyber-101/vulnerability-scanner-overview/catagorize"
th_parent: "cyber-101/vulnerability-scanner-overview"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/vulnerability-scanner-overview"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/vulnerability-scanner-overview"]
---

{% include tryhackme-nav.html %}

Vulnerability scans can be categorized into many types; however, the major categorization of these scans are explained below:
**Authenticated vs. Unauthenticated Scans**

| **Authenticated Scans** | **Unauthenticated Scans** |
| --- | --- |
| The credentials of the subject host must be provided to the vulnerability scanner. | The vulnerability scanner does not require the host’s credentials; it only needs the IP address. |
| Identifies the vulnerabilities that can be exploited by the attackers having access to the host. | Identifies the vulnerabilities that can be exploited by an external attacker having no access to the subject host. |
| It provides a deeper visibility into the target system by scanning its configuration and installed applications. | It is less resource-intensive and straightforward to set up. |
| For example, scanning an internal database by providing its credentials to the vulnerability scanner. | For example, scanning a public-facing website for vulnerabilities that any user can exploit. |

**Internal vs. External Scans**

| **Internal Scans** | **External Scans** |
| --- | --- |
| Conducted from inside the network. | Conducted from outside the network. |
| It focuses on the vulnerabilities that can be exploited inside the network. | It focuses on the vulnerabilities that can be exploited from outside the network. |
| Identifies vulnerabilities that would be exposed to the attackers once they get inside the network. | Identifies the vulnerabilities exposed to the attacker from outside the network. |
