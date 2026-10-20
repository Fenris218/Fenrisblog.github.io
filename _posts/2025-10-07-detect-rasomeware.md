---
title: "Detect Rasomeware"
date: 2025-10-07 11:39:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "ransomware group activity for detection purposes can be divided into several steps."
media_subpath: /assets/img/tryhackme/2025-10-07-detect-rasomeware/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-post-exploitation/detect-rasomeware/
th_id: "soc-lv-2/active-directory/detecting-ad-post-exploitation/detect-rasomeware"
th_parent: "soc-lv-2/active-directory/detecting-ad-post-exploitation"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-post-exploitation"]
---

{% include tryhackme-nav.html %}

ransomware group activity for detection purposes can be divided into several steps.

![image.png](image.png)

## **Pre-Encryption Detection**

We review how to detect the main techniques used during the pre-encryption stage.

**Delete Volume Shadow Copies**Organisations often use Volume Shadow Copy Service (VSS) for data backup purposes. Threat actors typically delete these shadow copies and disable the service to prevent recovery. (eventID : sysmon 1 and eventlog 4688)

**Disable Windows Recovery**

In cases where the system cannot boot normally due to crashes, corrupted files, or boot errors - which quite often occur during ransomware attacks - users attempt to utilise the Windows Recovery mechanism. Therefore, attackers frequently disable this capability before deploying ransomware.

**Delete Backups**

Organisations with robust backup infrastructure can mitigate the impact of encryption by restoring affected data, thereby eliminating the need for a decryptor and negating any potential ransom payment. Recognising this, threat actors systematically identify and destroy backup repositories prior to the encryption processes to maximise leverage over victims.

This activity can be observed in Sysmon EventID 1 or Windows Event Logs Security EventID 4688.

![image.png](image%201.png)

## **Detection of Ransomware Deployment Using GPO**

Group Policy Objects are a very convenient option for attackers to spread ransomware, as they provide the ability to execute specific actions across entire Organisational Units.

![image.png](image%202.png)

**SYSVOL** (System Volume) là một **thư mục đặc biệt trên Domain Controller (DC) của Active Directory**, dùng chủ yếu để lưu trữ và **replicate các file liên quan đến Group Policy và logon scripts** giữa các DC.

Let's imagine an attacker has already obtained Domain Admin through privilege escalation. What can we detect next? Let's examine this now. The threat actor needs to upload a Ransom file to SYSVOL. As you can see, the Office364.exe file was created in the scripts folder, after which the attacker proceeded to create a new GPO.

![image.png](image%203.png)

After that, the attacker needs to select a method to launch the ransom file. In our case, this is StartUp. As a result, the attacker adds a condition to this GPO to launch the file on systems in the TrySaveMe domain using StartUp.

![image.png](image%204.png)

còn nhiều thứ khác tại [TryHackMe | Detecting AD Post-Exploitation](https://tryhackme.com/room/detectingadpostexploitation)
