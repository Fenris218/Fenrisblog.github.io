---
title: "Alert Reporting"
date: 2025-06-06 08:36:00 +0700
categories: ["TryHackMe", "SOC LV1", "Alert Reporting"]
tags: ["tryhackme", "alert-reporting"]
description: "Before closing or passing the alert to L2, you might have to report it. Depending on team standards and alert severity, instead of a short alert comment, you…"
media_subpath: /assets/img/tryhackme/2025-06-06-alert-reporting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/alert-reporting/
th_id: "soc-lv1/alert-reporting"
th_parent: "soc-lv1"
th_kind: module
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/alert-reporting"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

Before closing or passing the alert to L2, you might have to report it. Depending on team standards and alert severity, instead of a short alert comment, you can be required to document your investigation in detail, ensuring all relevant evidence is included. 

## **Report Format**

We recommend you follow the [**Five Ws**](https://en.wikipedia.org/wiki/Five_Ws) approach and include at least these items in the report:

- **Who**: Which user logs in, runs the command, or downloads the file
- **What**: What exact action or event sequence was performed
- **When**: When exactly did the suspicious activity start and ended
- **Where**: Which device, IP, or website was involved in the alert
- **Why**: The most important W, the reasoning for your final verdict
