---
title: "Tools (Challenging)"
date: 2025-06-27 17:57:00 +0700
categories: ["TryHackMe", "SOC LV1", "Pyramid of Pain"]
tags: ["tryhackme", "pyramid-of-pain"]
description: "At this stage, we have levelled﻿ up our detection capabilities against the artifacts. The attacker would most likely give up trying to break into your networ…"
media_subpath: /assets/img/tryhackme/2025-06-27-tools-challenging/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/pyramid-of-pain/tools-challenging/
th_id: "soc-lv1/pyramid-of-pain/tools-challenging"
th_parent: "soc-lv1/pyramid-of-pain"
th_kind: note
th_order: 5
th_course: "soc-lv1"
th_module: "soc-lv1/pyramid-of-pain"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/pyramid-of-pain"]
---

{% include tryhackme-nav.html %}

At this stage, we have levelled﻿ up our detection capabilities against the artifacts. The attacker would most likely give up trying to break into your network or go back and try to create a new tool that serves the same purpose. It will be a game over for the attackers as they would need to invest some money into building a new tool (if they are capable of doing so), find the tool that has the same potential, or even gets some training to learn how to be proficient in a certain tool.

Attackers would use the utilities to create malicious macro documents (maldocs) for spearphishing attempts, a backdoor that can be used to establish [C2 (Command and Control Infrastructure)](https://www.varonis.com/blog/what-is-c2/), any custom .EXE, and .DLL files, payloads, or password crackers.

Antivirus signatures, detection rules, and YARA rules can be great weapons for you to use against attackers at this stage.

- [MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources to provide you with access to the samples, malicious feeds, and YARA results - these all can be very helpful when it comes to threat hunting and incident response.
- For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a great platform, where security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries.
- Fuzzy hashing is also a strong weapon against the attacker's tools. Fuzzy hashing helps you to perform similarity analysis - match two files with minor differences based on the fuzzy hash values. One of the examples of fuzzy hashing is the usage of [SSDeep](https://ssdeep-project.github.io/ssdeep/index.html); on the SSDeep official website, you can also find the complete explanation for fuzzy hashing. Example of SSDeep from VirusTotal:

![image.png](image.png)
