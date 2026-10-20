---
title: "Type of IDS"
date: 2025-05-20 15:19:00 +0700
categories: ["TryHackMe", "Cyber 101", "IDS Fundamental"]
tags: ["tryhackme", "ids-fundamental"]
description: "• Host Intrusion Detection System (HIDS): Host-based IDS solutions are installed individually on the hosts and are responsible for only detecting potential s…"
media_subpath: /assets/img/tryhackme/2025-05-20-type-of-ids/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/ids-fundamental/type-of-ids/
th_id: "cyber-101/ids-fundamental/type-of-ids"
th_parent: "cyber-101/ids-fundamental"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/ids-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/ids-fundamental"]
---

{% include tryhackme-nav.html %}

## **Deployment Modes**

• **Host Intrusion Detection System (HIDS):** Host-based IDS solutions are installed individually on the hosts and are responsible for only detecting potential security threats associated with that particular host. They provide detailed visibility of the host’s activities. However, host intrusion detection systems can be challenging to manage in large networks as they are resource-intensive and require management on each host.

• **Network Intrusion Detection System (NIDS):** Network-based IDS solutions are crucial in detecting potentially malicious activities within the whole network, regardless of any specific hosts. They monitor the network traffic of all the hosts involved to detect suspicious activities. It provides a centralized view of all the detections inside the whole network.

## **Detection Modes**

- **Signature-Based IDS:** Many attacks occur every day. Each attack has its unique pattern, which is known as a signature. These signatures are preserved by the IDS in their databases so that if the same attack happens in the future, it gets detected by its signature and reported to the security administrators for action. The stronger the signature database of the IDS is, the more efficiently it will detect known threats.
- **Anomaly-Based IDS:**
    - IDS **học cách hệ thống/mạng hoạt động bình thường** → gọi là **baseline**
    - Sau đó, nếu thấy **hành vi khác với bình thường** → **báo động (alert)**
    - Ưu điểm: **Phát hiện được zero-day attack,** Vì **không cần chữ ký (signature) sẵn có.**
    - Nhược điểm : Nhiều false positive
- **Hybrid IDS:** = Signature-Based IDS + Anomaly-Based IDS
