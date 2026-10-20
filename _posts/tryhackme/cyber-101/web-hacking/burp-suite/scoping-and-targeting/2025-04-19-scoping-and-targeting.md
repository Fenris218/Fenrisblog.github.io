---
title: "Scoping and Targeting"
date: 2025-04-19 08:48:00 +0700
categories: ["TryHackMe", "Cyber 101", "Web Hacking"]
tags: ["tryhackme", "web-hacking"]
description: "Capturing and logging all of the traffic can quickly become overwhelming and inconvenient, especially when we only want to focus on specific web applications…"
media_subpath: /assets/img/tryhackme/2025-04-19-scoping-and-targeting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/web-hacking/burp-suite/scoping-and-targeting/
th_id: "cyber-101/web-hacking/burp-suite/scoping-and-targeting"
th_parent: "cyber-101/web-hacking/burp-suite"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/web-hacking"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/web-hacking", "cyber-101/web-hacking/burp-suite"]
---

{% include tryhackme-nav.html %}

Capturing and logging all of the traffic can quickly become overwhelming and inconvenient, especially when we only want to focus on specific web applications. This is where scoping comes in.

By setting a scope for the project, we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) we want to test. The easiest way to do this is by switching to the `Target` tab, right-clicking on our target from the list on the left, and selecting `Add To Scope`. Burp will then prompt us to choose whether we want to stop logging anything that is not in scope, and in most cases, we want to select `yes`.
