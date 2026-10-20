---
title: "Domain Names (Simple)"
date: 2025-06-25 15:55:00 +0700
categories: ["TryHackMe", "SOC LV1", "Pyramid of Pain"]
tags: ["tryhackme", "pyramid-of-pain"]
description: "Domain Names can be thought as simply mapping an IP address to a string of text. A domain name can contain a domain and a top-level domain (e.g. evilcorp.com…"
media_subpath: /assets/img/tryhackme/2025-06-25-domain-names-simple/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/pyramid-of-pain/domain-names-simple/
th_id: "soc-lv1/pyramid-of-pain/domain-names-simple"
th_parent: "soc-lv1/pyramid-of-pain"
th_kind: note
th_order: 3
th_course: "soc-lv1"
th_module: "soc-lv1/pyramid-of-pain"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/pyramid-of-pain"]
---

{% include tryhackme-nav.html %}

Domain Names can be thought as simply mapping an IP address to a string of text. A domain name can contain a domain and a top-level domain (e.g. `evilcorp.com` ) or a sub-domain followed by a domain and top-level domain (e.g. `tryhackme.evilcorp.com` ). But we will not go into the details of how the Domain Name System (DNS) works. You can learn more about DNS in this ["DNS in Detail" Room](https://tryhackme.com/room/dnsindetail) . 

Domain Names can be a little more of a pain for the attacker to change as they would most likely need to purchase the domain, register it and modify DNS records. Unfortunately for defenders, many DNS providers have loose standards and provide APIs to make it even easier for the attacker to change the domain.

**Malicious**  Sodinokibi  **C2 ( Command and Control Infrastructure)  domains:**

![image.png](image.png)
