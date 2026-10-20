---
title: "EDR Telemetry"
date: 2025-06-15 17:45:00 +0700
categories: ["TryHackMe", "SOC LV1", "EDR"]
tags: ["tryhackme", "edr"]
description: "In the previous task, we learned about EDR agents, which collect different data from their endpoints and push it to the EDR console. This data is known as Te…"
media_subpath: /assets/img/tryhackme/2025-06-15-edr-telemetry/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/edr/edr-telemetry/
th_id: "soc-lv1/edr/edr-telemetry"
th_parent: "soc-lv1/edr"
th_kind: note
th_order: 4
th_course: "soc-lv1"
th_module: "soc-lv1/edr"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/edr"]
---

{% include tryhackme-nav.html %}

## **What is Telemetry?**

In the previous task, we learned about EDR agents, which collect different data from their endpoints and push it to the EDR console. This data is known as Telemetry. Telemetry is the black box of an endpoint with everything necessary for detection and investigation.

## **Collected Telemetry**

Usually, many activities are going on in the endpoints, most of which are legitimate. It is often difficult to differentiate between regular and malicious activity. The more data is collected, the better judgments can be made. EDR collects detailed telemetry from the endpoints. Let's take a brief look at some of the telemetry that it collects:

![image.png](image.png)

- **Process Executions and Terminations**It keeps track of all the running and idle processes, which helps to identify suspicious child-parent process relationships, suspicious executables initiating a process, malware payload, etc.
- **Network Connections**All the endpoints' network connections are monitored, which helps identify any connection to a C2 server, unusual port usage, data exfiltration, or lateral movement within the network.
- **Command Line Activity**It captures all the commands executed on the endpoints in CMD, PowerShell, etc., which helps to identify malicious command execution, obfuscated PowerShell script executions, which are often missed by a traditional antivirus.
- **Files and Folders Modifications**Threat actors modify different files and folders during data staging, ransomware executions, and malicious file dropping. The EDR tracks this.
- **Registry Modifications**The registry is a goldmine of information about the configurations in a Windows system. There are many registry modifications that occur during a malicious activity, and most of these are monitored by the EDR.

EDR collects much more than this data from an endpoint. It uses complex logic and machine learning algorithms to assess the activities. Advanced threats keep most of their activities stealthy, using legitimate utilities during execution. Individually, their activities may seem harmless, but when observed through detailed telemetry, they tell a different story. This detailed telemetry not only helps the EDR detect advanced threats and make better judgments on the legitimacy of the activities, but it is also very helpful for the analysts during the investigations. The analysts can understand the full chain of events, identify the root cause, and reconstruct the attack timeline.
