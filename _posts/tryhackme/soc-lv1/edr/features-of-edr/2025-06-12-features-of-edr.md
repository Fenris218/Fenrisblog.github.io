---
title: "Features of EDR"
date: 2025-06-12 14:42:00 +0700
categories: ["TryHackMe", "SOC LV1", "EDR"]
tags: ["tryhackme", "edr"]
description: "Visibility"
media_subpath: /assets/img/tryhackme/2025-06-12-features-of-edr/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/edr/features-of-edr/
th_id: "soc-lv1/edr/features-of-edr"
th_parent: "soc-lv1/edr"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/edr"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/edr"]
---

{% include tryhackme-nav.html %}

![image.png](image.png)

**Visibility** 

The level of visibility EDR provides is impressive. It collects detailed data from the endpoints, which includes process modifications, registry modifications, file and folder modifications, user actions, and much more. It then presents this information in a very structured format to the analyst. The analyst can see the whole process tree with a complete activity timeline of the sequence of actions. The analyst can also access the historical data of any endpoint for threat hunting or any other purpose. 

![image.png](image%201.png)

**Detection** 

The detection feature of EDR wins over traditional detection capabilities. It incorporates signature-based detections as well as behavior-based detections, such as unexpected user activities. With modern machine learning capabilities, it identifies any deviation from the baseline behavior and instantly flags it. It can also detect fileless malware that resides in memory. It also allows us to feed custom IOCs for threat detections.

![image.png](image%202.png)

**Response** 

EDR also empowers analysts to take action on detected threats. These actions can be taken at any endpoint within the central EDR console. 

![image.png](image%203.png)
