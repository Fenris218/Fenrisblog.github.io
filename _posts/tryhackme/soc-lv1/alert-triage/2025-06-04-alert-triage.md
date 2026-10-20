---
title: "Alert Triage"
date: 2025-06-04 18:34:00 +0700
categories: ["TryHackMe", "SOC LV1", "Alert Triage"]
tags: ["tryhackme", "alert-triage"]
description: "Alert Management Platforms"
media_subpath: /assets/img/tryhackme/2025-06-04-alert-triage/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/alert-triage/
th_id: "soc-lv1/alert-triage"
th_parent: "soc-lv1"
th_kind: module
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/alert-triage"
th_size: 1
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

**Alert Management Platforms**

| **Solution** | **Examples** | **Description** |
| --- | --- | --- |
| SIEMSystem | Splunk ES, Elastic | SIEM have solid alert management capabilities and are a perfect choice for most SOC teams |
| EDR or NDR | MS Defender,CrowdStrike | While EDR and NDR provide their own alert dashboards, it is preferred to use SIEM or SOAR |
| SOAR System | Splunk SOAR,Cortex SOAR | Bigger SOC teams can use SOAR to aggregate and centralise alerts from multiple solutions |
| ITSMSystem | Jira,TheHive | Some teams may have a custom ticket management (ITSM) setup using a dedicated solution(The GIF above is taken from Trello, a simple tool that can be adapted to ITSM needs) |

[Alert Properties]({{ site.baseurl }}/tryhackme/soc-lv1/alert-triage/alert-properties/)

![image.png](image.png)
