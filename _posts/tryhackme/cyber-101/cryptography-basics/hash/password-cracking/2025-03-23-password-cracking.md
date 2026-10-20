---
title: "Password cracking"
date: 2025-03-23 17:21:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "You can’t “decrypt” password hashes. You have to crack the hashes by hashing many different inputs (such as rockyou.txt as it covers many possible passwords)…"
media_subpath: /assets/img/tryhackme/2025-03-23-password-cracking/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/hash/password-cracking/
th_id: "cyber-101/cryptography-basics/hash/password-cracking"
th_parent: "cyber-101/cryptography-basics/hash"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/hash"]
---

{% include tryhackme-nav.html %}

You can’t “decrypt” password hashes. You have to crack the hashes by hashing many different inputs (such as `rockyou.txt` as it covers many possible passwords), potentially adding the salt if there is one and comparing it to the target hash. Once it matches, you know what the password was. Tools like [Hashcat](https://hashcat.net/hashcat/) and [John the Ripper](https://www.openwall.com/john/) are commonly used for these purposes.

**Cracking Passwords with GPUs**
 Modern GPUs (Graphics Processing Units) have thousands of cores. Although they can’t do the same sort of work that a CPU can, they are very good at some mathematical calculations involved in hash functions. You can use a graphics card to crack many hash types quickly. Some hashing algorithms, such as Bcrypt, are designed so that hashing on a GPU does not provide any speed improvement over using a CPU; this helps them resist cracking.
