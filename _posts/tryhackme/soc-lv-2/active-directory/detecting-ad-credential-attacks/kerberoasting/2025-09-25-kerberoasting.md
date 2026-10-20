---
title: "Kerberoasting"
date: 2025-09-25 11:27:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "Attackers target service accounts through Kerberoasting because these accounts often have weak passwords and elevated privileges. And the attack itself requi…"
media_subpath: /assets/img/tryhackme/2025-09-25-kerberoasting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-credential-attacks/kerberoasting/
th_id: "soc-lv-2/active-directory/detecting-ad-credential-attacks/kerberoasting"
th_parent: "soc-lv-2/active-directory/detecting-ad-credential-attacks"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-credential-attacks"]
---

{% include tryhackme-nav.html %}

Attackers target service accounts through Kerberoasting because these accounts often have weak passwords and elevated privileges. And the attack itself requires nothing more than a regular domain user account.

## **How Do Accounts End Up Kerberoastable?**

It usually starts with an IT admin who needs to run a service, like SQL Server or a web application, and decides to use their own DA account (or a shared admin account) as the service identity because it's quick. They register an SPN on the account, set a short password so the team can remember it, and move on. Now that account has a weak password hash tied to an SPN that any domain user can request. Multiply this across years of admin decisions, and you get environments with dozens of Kerberoastable accounts.

When a user needs to access a service in Active Directory, they request a Kerberos service ticket (TGS) from the domain controller. The DC looks up the SPN, encrypts the ticket with the service account's password hash, and hands it back. Normally, the user presents the ticket to the service, and the service decrypts it to verify the user's identity.

The problem is that any domain user can request a service ticket for any SPN in the domain. The DC doesn't check whether the user actually intends to use the service. It just issues the ticket. An attacker takes that ticket and cracks the encryption offline. If the service account has a weak password, the attacker recovers the plaintext password in minutes. 

![image.png](image.png)

The detection centers on Event 4769 (Kerberos Service Ticket Requested), which the DC logs when it processes a TGS-REQ. Modern AD environments default to AES-256 encryption (`0x12`) for Kerberos tickets. Most Kerberoasting tools, including Rubeus and Impacket's `GetUserSPNs.py`, downgrade the request to RC4 encryption (`0x17`) because RC4 hashes are much faster to crack. A TGS request with `Ticket_Encryption_Type=0x17` in an environment that uses AES is a strong indicator.

Here are the fields in Event 4769 that matter for detection:

Normal Kerberos traffic includes a lot of Event 4769 entries. Computer accounts (names ending in `$`) and `krbtgt` requests generate high volumes as part of regular domain operations. We exclude both to focus on service accounts that could be Kerberoasting targets.

Overall trend is toward AES-only environments. This means RC4-based detection alone isn't enough for the long term
