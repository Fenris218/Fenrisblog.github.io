---
title: "Log Sources and Ingestion"
date: 2025-05-13 08:12:00 +0700
categories: ["TryHackMe", "Cyber 101", "SIEM"]
tags: ["tryhackme", "siem"]
description: "Windows records every event that can be viewed through the Event Viewer."
media_subpath: /assets/img/tryhackme/2025-05-13-log-sources-and-ingestion/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/siem/log-sources-and-ingestion/
th_id: "cyber-101/siem/log-sources-and-ingestion"
th_parent: "cyber-101/siem"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/siem"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/siem"]
---

{% include tryhackme-nav.html %}

### **Windows Machine**

Windows records every event that can be viewed through the Event Viewer.

### **Linux Machine**

Linux OS stores all the related logs, such as events, errors, warnings, etc. These are then ingested into SIEM for continuous monitoring. Some of the common locations where Linux stores logs are:

- /var/log/httpd: Contains HTTP Request / Response and error logs.
- /var/log/cron: Events related to cron jobs are stored in this location. (**Cron job** là một **tác vụ (job) được chạy tự động theo lịch)**
- /var/log/auth.log and /var/log/secure: Stores authentication-related logs.
- /var/log/kern: This file stores kernel-related events.

## Log Ingestion ( quá trình thu thập log và đưa vào phân tích )

Each SIEM solution has its own way of ingesting the logs. Some common methods used by these SIEM solutions are explained below:

1. Agent / ForwarderThese SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed on the Endpoint. It is configured to capture and send all the important logs to the SIEM server.
2. **Syslog**Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., and send real-time data to the centralized destination.
3. **Manual Upload**Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.
4. **Port-Forwarding**SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.
