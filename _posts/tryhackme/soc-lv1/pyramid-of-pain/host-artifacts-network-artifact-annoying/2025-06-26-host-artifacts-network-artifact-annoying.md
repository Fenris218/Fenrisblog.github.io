---
title: "Host Artifacts / Network Artifact(Annoying)"
date: 2025-06-26 16:56:00 +0700
categories: ["TryHackMe", "SOC LV1", "Pyramid of Pain"]
tags: ["tryhackme", "pyramid-of-pain"]
description: "On this level, the attacker will feel a little more annoyed and frustrated if you can detect the attack. The attacker would need to circle back at this detec…"
media_subpath: /assets/img/tryhackme/2025-06-26-host-artifacts-network-artifact-annoying/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/pyramid-of-pain/host-artifacts-network-artifact-annoying/
th_id: "soc-lv1/pyramid-of-pain/host-artifacts-network-artifact-annoying"
th_parent: "soc-lv1/pyramid-of-pain"
th_kind: note
th_order: 4
th_course: "soc-lv1"
th_module: "soc-lv1/pyramid-of-pain"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/pyramid-of-pain"]
---

{% include tryhackme-nav.html %}

On this level, the attacker will feel a little more annoyed and frustrated if you can detect the attack. The attacker would need to circle back at this detection level and change his attack tools and methodologies. This is very time-consuming for the attacker.

Host artifacts are the traces or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything exclusive to the current threat.

Network artifacts can be detected in Wireshark PCAPs  by using a network protocol analyzer such as [TShark](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) or exploring IDS (Intrusion Detection System) logging from a source such as [Snort](https://www.snort.org/).
