---
title: "Technology"
date: 2025-05-07 14:06:00 +0700
categories: ["TryHackMe", "Cyber 101", "SOC Fundamental"]
tags: ["tryhackme", "soc-fundamental"]
description: "Security solutions centralize all the information of the devices or applications present in the network and automate the detection and response capabilities."
media_subpath: /assets/img/tryhackme/2025-05-07-technology/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/soc-fundamental/technology/
th_id: "cyber-101/soc-fundamental/technology"
th_parent: "cyber-101/soc-fundamental"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/soc-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/soc-fundamental"]
---

{% include tryhackme-nav.html %}

Security solutions centralize all the information of the devices or applications present in the network and automate the detection and response capabilities.

Let's get a brief understanding of some of these security solutions:

• **SIEM:** Security Information and Event Management (SIEM) is a popular tool used in almost every SOC environment. This tool collects logs from various network devices, referred to as log sources. Detection rules are configured in the SIEM solution, which contains logic to identify suspicious activity. The SIEM solution provides us with the detections after correlating them with multiple log sources and alerts us in case of a match with any of the rules. Modern SIEM solutions surpass this rule based detection analysis, providing us with user behavior analytics and threat intelligence capability. Machine learning algorithms support this to enhance the detection capabilities.

**Note:** The SIEM solution only provides the **Detection** capabilities in a SOC environment.

- **EDR:** Endpoint Detection and Response (EDR) provides the SOC team with detailed real-time and historical visibility of the devices’ activities. It operates on the endpoint level and can carry out automated responses. EDR has extensive detection capabilities for endpoints, allowing you to investigate them in detail and respond with a few clicks.
- **Firewall:** A firewall functions purely for network security and acts as a barrier between your internal and external networks (such as the Internet). It monitors incoming and outgoing network traffic and filters any unauthorized traffic. The firewall also has some detection rules deployed, which help us identify and block suspicious traffic before it reaches the internal network.

Several other security solutions play unique roles in a SOC environment, such as Antivirus, EPP, IDS/IPS, XDR, SOAR, and more. The decision on what Technology to deploy in the SOC comes after careful consideration of the threat surface and the available resources in the organization.
