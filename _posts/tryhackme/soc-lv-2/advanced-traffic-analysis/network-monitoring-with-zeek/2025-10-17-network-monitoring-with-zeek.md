---
title: "Network Monitoring with Zeek"
date: 2025-10-17 09:49:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Traffic Analysis"]
tags: ["tryhackme", "advanced-traffic-analysis"]
description: "Zeek is a passive network monitor that watches, parses, and writes structured log entries for every connection, every DNS query, every TLS handshake, and eve…"
media_subpath: /assets/img/tryhackme/2025-10-17-network-monitoring-with-zeek/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-traffic-analysis/network-monitoring-with-zeek/
th_id: "soc-lv-2/advanced-traffic-analysis/network-monitoring-with-zeek"
th_parent: "soc-lv-2/advanced-traffic-analysis"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-traffic-analysis"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-traffic-analysis"]
---

{% include tryhackme-nav.html %}

Zeek is a passive network monitor that watches, parses, and writes structured log entries for every connection, every DNS query, every TLS handshake, and every file transfer it sees. Each protocol analyser produces its own log file, and every entry from the same network session shares a unique identifier called a `uid`. An analyst who follows that `uid` across the log set can reconstruct the entire session without ever touching a packet
