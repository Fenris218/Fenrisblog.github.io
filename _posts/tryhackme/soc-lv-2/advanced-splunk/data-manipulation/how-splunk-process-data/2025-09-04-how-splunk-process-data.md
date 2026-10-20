---
title: "How Splunk process data"
date: 2025-09-04 14:06:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: ""
media_subpath: /assets/img/tryhackme/2025-09-04-how-splunk-process-data/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/data-manipulation/how-splunk-process-data/
th_id: "soc-lv-2/advanced-splunk/data-manipulation/how-splunk-process-data"
th_parent: "soc-lv-2/advanced-splunk/data-manipulation"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/data-manipulation"]
---

{% include tryhackme-nav.html %}

- inputs.conf :  file instructs Splunk on what data to ingest, where it originates, how to collect it, and what basic metadata to assign, such as `sourcetype`, `host`, or `source`
- props.conf :  file defines data parsing settings for specific source types or data sources within Splunk. You can define custom field extractions in `props.conf` by specifying the source type, field extraction name, and a custom regular expression
