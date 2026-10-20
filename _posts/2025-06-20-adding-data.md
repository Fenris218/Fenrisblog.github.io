---
title: "Adding Data"
date: 2025-06-20 10:50:00 +0700
categories: ["TryHackMe", "SOC LV1", "Splunk: The Basics"]
tags: ["tryhackme", "splunk-the-basics"]
description: "Splunk can ingest any data. According to the Splunk documentation, when data is added to Splunk, the data is processed and transformed into a series of indiv…"
media_subpath: /assets/img/tryhackme/2025-06-20-adding-data/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/splunk-the-basics/adding-data/
th_id: "soc-lv1/splunk-the-basics/adding-data"
th_parent: "soc-lv1/splunk-the-basics"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/splunk-the-basics"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/splunk-the-basics"]
---

{% include tryhackme-nav.html %}

Splunk can ingest any data. According to the Splunk documentation, when data is added to Splunk, the data is processed and transformed into a series of individual events. The data sources can be event logs, website logs, firewall logs, etc. The data sources are grouped into categories.

![image.png](image.png)

In this task, we're going to focus on **VPN logs**. We're presented with the following screen when we click on the `Add Data` link on the Splunk home screen.

https://tryhackme.com/room/splunk101

![image.png](image%201.png)
