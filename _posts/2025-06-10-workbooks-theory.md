---
title: "Workbooks Theory"
date: 2025-06-10 12:40:00 +0700
categories: ["TryHackMe", "SOC LV1", "SOC Workbooks and Lookups"]
tags: ["tryhackme", "soc-workbooks-and-lookups"]
description: "SOC workbook, also called playbook, runbook, or workflow, is a structured document that defines the steps required to investigate and remediate specific thre…"
media_subpath: /assets/img/tryhackme/2025-06-10-workbooks-theory/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/soc-workbooks-and-lookups/workbooks-theory/
th_id: "soc-lv1/soc-workbooks-and-lookups/workbooks-theory"
th_parent: "soc-lv1/soc-workbooks-and-lookups"
th_kind: note
th_order: 3
th_course: "soc-lv1"
th_module: "soc-lv1/soc-workbooks-and-lookups"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/soc-workbooks-and-lookups"]
---

{% include tryhackme-nav.html %}

## **SOC Workbooks**

**SOC workbook**, also called playbook, runbook, or workflow, is a structured document that defines the steps required to investigate and remediate specific threats efficiently and consistently. Since L1 analysts are considered junior specialists and are not expected to triage every possible attack scenario perfectly, senior analysts often prepare workbooks to support their less experienced teammates. L1 analysts are recommended and sometimes even required to triage the alerts precisely according to workbooks to avoid mistakes and streamline the analysis.

![image.png](image.png)

The diagram above is a typical example of an investigation workbook aimed to help L1 analysts triage alerts about atypical email, web, or corporate VPN login. Most workbook diagrams are supplemented with a detailed textual guide and links to the mentioned resources. Also, note how the workbook is divided into three logical groups. By following the steps in the correct order, you can guarantee high-quality alert triage and eliminate cases where the verdict is made without enough evidence:

1. **Enrichment**: Use Threat Intelligence and identity inventory to get information about the affected user
2. **Investigation**: Using the gathered data and SIEM logs, make your verdict if the login is expected
3. **Escalation**: Escalate the alert to L2 or communicate the login with the user if necessary
