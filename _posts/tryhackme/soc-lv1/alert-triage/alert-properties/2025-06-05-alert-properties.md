---
title: "Alert Properties"
date: 2025-06-05 19:35:00 +0700
categories: ["TryHackMe", "SOC LV1", "Alert Triage"]
tags: ["tryhackme", "alert-triage"]
description: ""
media_subpath: /assets/img/tryhackme/2025-06-05-alert-properties/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/alert-triage/alert-properties/
th_id: "soc-lv1/alert-triage/alert-properties"
th_parent: "soc-lv1/alert-triage"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/alert-triage"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/alert-triage"]
---

{% include tryhackme-nav.html %}

| **№** | **Property** | **Description** | **Examples** |
| --- | --- | --- | --- |
| **1** | Alert Time | Shows alert creation time. Alert usually triggers a few minutes after the actual event | • Alert Time: March 21, 15:35<br>• Event Time: March 21, 15:32 |
| **2** | Alert Name | Provides a summary of what happened, based on the detection rule's name | • Unusual Login Location<br>• Email Marked as Phishing<br>• Windows RDP Bruteforce<br>• Potential Data Exfiltration |
| **3** | Alert Severity | Defines the urgency of the alert,initially set by detection engineers,but can be altered by analysts if needed | • (🟢) Low / Informational<br>• (🟡) Medium / Moderate<br>• (🟠) High / Severe<br>• (🔴) Critical / Urgent |
| **4** | Alert Status | Informs if somebody is working on the alert or if the triage is done | • (🆕) New / Unassigned<br>• (🔄) In Progress / Pending<br>• (✅) Closed / Resolved<br>• And often other custom statuses |
| **5** | Alert Verdict | Also called alert classification,explains if the alert is a real threat or noise | • (🔴) True Positive / Real Threat<br>• (🟢) False Positive / No Threat<br>• And often other custom verdicts |
| **6** | Alert Assignee | Shows the analyst that was assigned or assigned themselves to review the alert | • Assignee can sometimes be called alert owner<br>• Assignee takes responsibility for their alerts |
| **7** | Alert Description | Explains what the alert is about,usually in three sections on the right | • The logic of the alert generating rule<br>• Why this activity can indicate an attack<br>• Optionally, how to triage this alert |
| **8** | Alert Fields | Provides SOC analysts' comments and values on which the alert was triggered | • Affected Hostname<br>• Entered Commandline<br>• And many more, depending on the alert |
