---
title: "Site map and Issue Definitions"
date: 2025-04-18 19:47:00 +0700
categories: ["TryHackMe", "Cyber 101", "Web Hacking"]
tags: ["tryhackme", "web-hacking"]
description: "The Target tab in Burp Suite provides more than just control over the scope of our testing. It consists of three sub-tabs:"
media_subpath: /assets/img/tryhackme/2025-04-18-site-map-and-issue-definitions/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/web-hacking/burp-suite/site-map-and-issue-definitions/
th_id: "cyber-101/web-hacking/burp-suite/site-map-and-issue-definitions"
th_parent: "cyber-101/web-hacking/burp-suite"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/web-hacking"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/web-hacking", "cyber-101/web-hacking/burp-suite"]
---

{% include tryhackme-nav.html %}

The **Target** tab in Burp Suite provides more than just control over the scope of our testing. It consists of three sub-tabs:

1. **Site map**: This sub-tab allows us to map out the web applications we are targeting in a tree structure. Every page that we visit while the proxy is active will be displayed on the site map. 
2. **Issue definitions: is a** section provides an extensive list of web vulnerabilities, complete with descriptions and references.
3. **Scope settings**: This setting allows us to control the target scope in Burp Suite. It enables us to include or exclude specific domains/IPs to define the scope of our testing. By managing the scope, we can focus on the web applications we are specifically targeting and avoid capturing unnecessary traffic.
