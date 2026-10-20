---
title: "AS-REP roasting"
date: 2025-09-26 12:28:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "AS-REP Roasting targets a different weakness entirely: user accounts with preauthentication disabled. It doesn't require SPNs, and unlike Kerberoasting, the…"
media_subpath: /assets/img/tryhackme/2025-09-26-as-rep-roasting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-credential-attacks/as-rep-roasting/
th_id: "soc-lv-2/active-directory/detecting-ad-credential-attacks/as-rep-roasting"
th_parent: "soc-lv-2/active-directory/detecting-ad-credential-attacks"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-credential-attacks"]
---

{% include tryhackme-nav.html %}

AS-REP Roasting targets a different weakness entirely: user accounts with preauthentication disabled. It doesn't require SPNs, and unlike Kerberoasting, the attacker doesn't even need valid domain credentials to perform it. 

The underlying flaw is the same, though: the DC hands back encrypted material that the attacker can crack offline to recover the plaintext password. The difference is what triggers the DC to hand it over and what it's encrypted with.

The user encrypts a timestamp with their password hash and sends it along with the AS-REQ. The DC decrypts it, verifies the timestamp is recent, and only then issues the TGT. The DC logs Event 4768 (Kerberos TGT Request) with `Pre_Authentication_Type=2`, followed by Event 4769 when the user requests a service ticket, and Event 4624 when they log onto the target service. 

![image.png](image.png)

On the other hand, when an account has the `DONT_REQUIRE_PREAUTH` flag enabled, the DC skips that verification step. It issues the TGT without first confirming the requester knows the password. The AS-REP that comes back is encrypted with the account's password hash, which means an attacker can take it offline and crack it to recover the plaintext password.

![image.png](image%201.png)

This misconfiguration exists because some legacy applications, like older ERP or payroll systems, fail Kerberos authentication unless preauth is disabled for their service account. Admins might disable it to get the application working and then forget about it.

The key difference between AS-REP Roasting and the normal flow is that the attacker requests the TGT purely to extract the crackable hash. They never request a service ticket, and they never log onto anything. So the DC logs Event 4768 with `Pre_Authentication_Type=0`, but there is no 4769 and no 4624

![image.png](image%202.png)
