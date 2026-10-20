---
title: "IDS Fundamental"
date: 2025-05-19 14:18:00 +0700
categories: ["TryHackMe", "Cyber 101", "IDS Fundamental"]
tags: ["tryhackme", "ids-fundamental"]
description: "If an attacker successfully bypasses a firewall via a legitimate-looking connection and then performs any malicious activities inside the network, there shou…"
media_subpath: /assets/img/tryhackme/2025-05-19-ids-fundamental/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/ids-fundamental/
th_id: "cyber-101/ids-fundamental"
th_parent: "cyber-101"
th_kind: module
th_order: 16
th_course: "cyber-101"
th_module: "cyber-101/ids-fundamental"
th_size: 3
th_ancestors: ["cyber-101"]
---

{% include tryhackme-nav.html %}

If an attacker successfully bypasses a firewall via a legitimate-looking connection and then performs any malicious activities inside the network, there should be something to detect it in a timely manner. For this purpose, we have a security solution inside the network. This solution is known as an `Intrusion Detection System (IDS)`.

It  monitors the network traffic based on its signature and anomaly-based detections, and detects any abnormal traffic going out or inside the network. Upon every detection, an alert is generated for the security administrators. IDS does not act on those detections; it only notifies the security administrators about the malicious activity.

[Type of IDS]({{ site.baseurl }}/tryhackme/cyber-101/ids-fundamental/type-of-ids/)

[IDS Example: Snort]({{ site.baseurl }}/tryhackme/cyber-101/ids-fundamental/ids-example-snort/)

[Snort Usage]({{ site.baseurl }}/tryhackme/cyber-101/ids-fundamental/snort-usage/)
