---
title: "Elastic Stack: The Basics"
date: 2025-06-21 11:51:00 +0700
categories: ["TryHackMe", "SOC LV1", "Elastic Stack: The Basics"]
tags: ["tryhackme", "elastic-stack-the-basics"]
description: ""
media_subpath: /assets/img/tryhackme/2025-06-21-elastic-stack-the-basics/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/elastic-stack-the-basics/
th_id: "soc-lv1/elastic-stack-the-basics"
th_parent: "soc-lv1"
th_kind: module
th_order: 7
th_course: "soc-lv1"
th_module: "soc-lv1/elastic-stack-the-basics"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

![image.png](image.png)

- Elasticsearch : search
- logstash : dùng để **thu thập, xử lý và chuyển tiếp log** trước khi đưa vào **Elasticsearch**.
- Beats : dùng để **thu thập dữ liệu từ máy nguồn và gửi về Logstash hoặc Elasticsearch** trong Elastic Stack.
- Kibana :  web-based data visualization tool that works with Elasticsearch to analyze, investigate, and visualize data streams in real time.
