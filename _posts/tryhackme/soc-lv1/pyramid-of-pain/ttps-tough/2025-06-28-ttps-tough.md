---
title: "TTPs (Tough)"
date: 2025-06-28 18:58:00 +0700
categories: ["TryHackMe", "SOC LV1", "Pyramid of Pain"]
tags: ["tryhackme", "pyramid-of-pain"]
description: "TTPs stands for Tactics, Techniques & Procedures. This includes the whole MITRE ATT&CK Matrix, which means all the steps taken by an adversary to achieve his…"
media_subpath: /assets/img/tryhackme/2025-06-28-ttps-tough/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/pyramid-of-pain/ttps-tough/
th_id: "soc-lv1/pyramid-of-pain/ttps-tough"
th_parent: "soc-lv1/pyramid-of-pain"
th_kind: note
th_order: 6
th_course: "soc-lv1"
th_module: "soc-lv1/pyramid-of-pain"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/pyramid-of-pain"]
---

{% include tryhackme-nav.html %}

TTPs stands for Tactics, Techniques & Procedures. This includes the whole [MITRE ATT&CK Matrix](https://attack.mitre.org/), which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration. 

If you can detect and respond to the TTPs quickly, you leave the adversaries almost no chance to fight back. For, example if you could detect a [Pass-the-Hash](https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack) attack using Windows Event Log Monitoring and remediate it, you would be able to find the compromised host very quickly and stop the lateral movement inside your network. At this point, the attacker would have two options:

1. Go back, do more research and training, reconfigure their custom tools
2. Give up and find another target
