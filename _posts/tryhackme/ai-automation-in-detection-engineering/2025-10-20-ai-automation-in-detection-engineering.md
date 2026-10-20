---
title: "AI& Automation in Detection Engineering"
date: 2025-10-20 12:52:00 +0700
categories: ["TryHackMe", "AI& Automation in Detection Engineering"]
tags: ["tryhackme"]
description: "Có một đoạn trong vòng đời của detection mà detection engineer có thể xây dựng thành một quy trình tự động, lặp lại được."
media_subpath: /assets/img/tryhackme/2025-10-20-ai-automation-in-detection-engineering/
toc: true
comments: false
hidden: true
permalink: /tryhackme/ai-automation-in-detection-engineering/
th_id: "ai-automation-in-detection-engineering"
th_parent: "root"
th_kind: course
th_order: 5
th_course: "ai-automation-in-detection-engineering"
th_module: ""
th_size: 0
th_ancestors: []
---

{% include tryhackme-nav.html %}

Có một đoạn trong vòng đời của detection mà detection engineer có thể **xây dựng thành một quy trình tự động, lặp lại được**.

Đoạn đó là: **Thiết kế rule → kiểm tra/test → review → deploy production → quản lý các thay đổi**
“Cỗ máy” để làm việc đó được gọi là **Detection-as-Code (DaC)**.

Thay vì SOC analyst vào Splunk/Sentinel rồi **tự tay tạo rule**, DaC biến detection thành một workflow giống software development:

With DaC, detection engineers treat a detection, usually a Sigma rule YAML file, as a file in a Git repository (like a code file), and apply the engineering strategies:

- **Version control (Git)**: Every change to every rule is tracked: who changed what, when, and why. You can compare versions and roll back instantly when something breaks. The repository, not the SIEM, becomes the single source of truth for your detections.
- **Peer review (pull requests)**: A pull request (PR) is a proposed change that a second engineer must approve before it is merged. Review stops being a favor you ask a colleague and becomes a normal, low-friction step.
- **Automated checks (a CI/CD pipeline)**: CI/CD (Continuous Integration/Continuous Deployment) is an automated assembly line that runs whenever you propose a change. For a detection, that line checks the rule's syntax, enforces your team's standards, and tests the rule against live data to estimate how noisy it will be. For example, that 60% jump in false positives would have been flagged by the pipeline at proposal time.

![image.png](image.png)
