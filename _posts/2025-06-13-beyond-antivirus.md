---
title: "Beyond Antivirus"
date: 2025-06-13 15:43:00 +0700
categories: ["TryHackMe", "SOC LV1", "EDR"]
tags: ["tryhackme", "edr"]
description: "Let's assume an airport is an endpoint that needs protection. One layer of protection is to check the passports of people when they pass through immigration.…"
media_subpath: /assets/img/tryhackme/2025-06-13-beyond-antivirus/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/edr/beyond-antivirus/
th_id: "soc-lv1/edr/beyond-antivirus"
th_parent: "soc-lv1/edr"
th_kind: note
th_order: 2
th_course: "soc-lv1"
th_module: "soc-lv1/edr"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/edr"]
---

{% include tryhackme-nav.html %}

## **Why do we need an EDR when we already have an Antivirus (AV) on the endpoints?**

Let's assume an airport is an endpoint that needs protection. One layer of protection is to check the passports of people when they pass through immigration. The immigration check (AV) monitors incoming people and matches their passports with a list of known criminals in its database. If there is a match, the entry is blocked and caught.

Sounds like a smart protection, right?

But, what happens if somebody who has never been identified as a criminal in the past and has an innocent personality tries to come in? The immigration check will let them in. Now, what if this innocent person were a professional thief trained to evade basic security? The airport has an undetected threat inside!

This is where an EDR comes in.

An EDR in this analogy would be the security officers stationed inside the airport (endpoint). These security officers would constantly monitor the security cameras and motion sensors in the airport (endpoint). Compared to the immigration check (AV), the security officers (EDR) enhance the protection of the airport (endpoint) through CCTV monitoring and motion sensors. Even if somebody manages to evade the immigration check, the security officers will constantly be monitoring their actions, such as:

- Are they roaming close to restricted areas?
- Is their behaviour suspicious?
- Are they leaving their bags somewhere unattended?

The security officers can also take action if something does not feel right to them or alert the airport management with complete details of what happened.

The Antivirus (AV) may detect some basic threats, but to detect advanced threats that evade normal detections, we need an EDR. Unlike antivirus software's basic signature-based detection, it monitors and records the behaviors of the endpoint. An EDR also provides organization-wide visibility of any activity. For example, if a suspicious file is detected on one endpoint, the EDR will also check it across all the other endpoints.

Let's examine an advanced malicious activity step by step on an endpoint and compare the response of an AV and EDR at each stage.

## **Scenario Breakdown**

- **Step #1:** A user receives a phishing email with a Word document embedded with a malicious macro (VBA script)
- **Step #2:** The user downloads the document and opens it
- **Step #3:** The malicious macro is silently executed, and it spawns PowerShell
- **Step #4:** The malicious macro runs an obfuscated PowerShell command to download a sophisticated second-stage payload
- **Step #5:** The payload is injected into a legitimate svchost.exe
- **Step #6:** The attacker gains remote access to the system

![image.png](image.png)
