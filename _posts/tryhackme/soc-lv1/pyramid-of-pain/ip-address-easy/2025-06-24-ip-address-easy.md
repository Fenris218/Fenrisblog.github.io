---
title: "IP Address (Easy)"
date: 2025-06-24 14:54:00 +0700
categories: ["TryHackMe", "SOC LV1", "Pyramid of Pain"]
tags: ["tryhackme", "pyramid-of-pain"]
description: "on the Pyramid of Pain, IP addresses are indicated with the color green."
media_subpath: /assets/img/tryhackme/2025-06-24-ip-address-easy/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/pyramid-of-pain/ip-address-easy/
th_id: "soc-lv1/pyramid-of-pain/ip-address-easy"
th_parent: "soc-lv1/pyramid-of-pain"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/pyramid-of-pain"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/pyramid-of-pain"]
---

{% include tryhackme-nav.html %}

on the Pyramid of Pain, IP addresses are indicated with the color green. 

From a defense standpoint, knowledge of the IP addresses an adversary uses can be valuable. A common defense tactic is to block, drop, or deny inbound requests from IP addresses on your parameter or external firewall. This tactic is often not bulletproof as it’s trivial for an experienced adversary to recover simply by using a new public IP address.

One of the ways an adversary can make it challenging to successfully carry out IP blocking is by using **Fast Flux**.
