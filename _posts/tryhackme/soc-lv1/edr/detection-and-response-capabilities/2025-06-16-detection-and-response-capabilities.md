---
title: "Detection And Response Capabilities"
date: 2025-06-16 18:46:00 +0700
categories: ["TryHackMe", "SOC LV1", "EDR"]
tags: ["tryhackme", "edr"]
description: "Based on the telemetry received from the endpoints, some advanced detection techniques are applied to this data. Some of these techniques include:"
media_subpath: /assets/img/tryhackme/2025-06-16-detection-and-response-capabilities/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/edr/detection-and-response-capabilities/
th_id: "soc-lv1/edr/detection-and-response-capabilities"
th_parent: "soc-lv1/edr"
th_kind: note
th_order: 5
th_course: "soc-lv1"
th_module: "soc-lv1/edr"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/edr"]
---

{% include tryhackme-nav.html %}

## **Detection**

Based on the telemetry received from the endpoints, some advanced detection techniques are applied to this data. Some of these techniques include:

- **Behavioral Detection:** Instead of just matching the signatures with known threats, it observes the complete behavior of a file. Advanced threats craft their malware to look clean and use legitimate processes to carry out their attack. EDR catches this behavior. **Example:** A process winword.exe spawning PowerShell.exe will be flagged by the EDR due to the behavior. A Word document spawning a PowerShell is an unusual parent-child relationship.
- **Anomaly Detection:** With time, EDR understands the baseline behavior of the endpoints. Any activity that deviates from this behavior will be flagged. During any malicious activity, the endpoint's behavior deviates from normal. EDR picks it up. Sometimes, this can generate false positives as well. **Example:** On one of the endpoints, a process modifies an auto-start registry key, which is not a common behavior on the endpoint.
- **IOC matching:** EDRs have some strong threat intelligence field integrations. Except for zero-day attacks, most of the attacks have indicators published in the threat intelligence feeds. EDR flags any activity that matches any known IOC. **Example:** A user downloads a file that drops an executable. The executable is often used in a specific attack. The hash of this executable will get matched with the threat intelligence feed and instantly flagged by the EDR.
- **MITRE ATT&CK Mapping:** Any activity flagged by the EDR is not only marked as malicious or suspicious but also mapped with the MITRE Tactic and Technique (attack stage) that the particular activity was on. This proves to be very helpful for the analysts. **Example:** If the EDR flags the creation of a scheduled task for any reason, it will likely map this activity to the following:
    - Tactic: Persistence
    - Technique: Scheduled Task/Job
- **Machine Learning Algorithms:** Advanced threat actors try to evade defenses as much as possible, and their activities may sometimes bypass advanced detection techniques. Modern EDRs have machine learning models trained by a large dataset of normal and malicious behaviors. This can detect complex patterns of an attack. **Example:** Attacks in which the individual actions are not inherently malicious, but the ML algorithm identifies the whole chain of activities as malicious. Fileless attacks and multi-staged intrusions are often detected through this.

## **Response**

EDR offers both automated and manual responses. You can make policies to block known malicious behaviors automatically. However, manual response gives you a wide range of response capabilities. Let's discuss some of them.

…
