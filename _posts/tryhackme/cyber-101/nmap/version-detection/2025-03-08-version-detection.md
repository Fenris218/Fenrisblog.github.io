---
title: "Version Detection"
date: 2025-03-08 14:06:00 +0700
categories: ["TryHackMe", "Cyber 101", "Nmap"]
tags: ["tryhackme", "nmap"]
description: ""
media_subpath: /assets/img/tryhackme/2025-03-08-version-detection/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/nmap/version-detection/
th_id: "cyber-101/nmap/version-detection"
th_parent: "cyber-101/nmap"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/nmap"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/nmap"]
---

{% include tryhackme-nav.html %}

- OS detection : -O ( xác định phiên bản OS)

![image.png](image.png)

- **Service and Version Detection:  -sV**

![image.png](image%201.png)

- **Forcing the Scan :** When we run our port scan, such as using `-sS`, there is a possibility that the target host does not reply during the host discovery phase (e.g. a host doesn’t reply to ICMP requests). Consequently, Nmap will mark this host as down and won’t launch a port scan against it. We can ask Nmap to treat all hosts as online and port scan every host, including those that didn’t respond during the host discovery phase. This choice can be triggered by adding the `-Pn` option

![image.png](image%202.png)
