---
title: "Cracking Hashes from /etc/shadow"
date: 2025-03-27 09:25:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "/etc/shadow file is the file on Linux machines where password hashes are stored. It also stores other information, such as the date of last password change a…"
media_subpath: /assets/img/tryhackme/2025-03-27-cracking-hashes-from-etc-shadow/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/cracking-hashes-from-etc-shadow/
th_id: "cyber-101/cryptography-basics/john-the-ripper/cracking-hashes-from-etc-shadow"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

`/etc/shadow` file is the file on Linux machines where password hashes are stored. It also stores other information, such as the date of last password change and password expiration information. This file is usually only accessible by the root user

John can be very particular about the formats it needs data in to be able to work with it; for this reason, to crack `/etc/shadow` passwords, you must combine it with the `/etc/passwd` file for John to understand the data it’s being given. To do this, we use a tool built into the John suite of tools called `unshadow`. The basic syntax of `unshadow` is as follows:

```bash
unshadow [path to passwd] [path to shadow] > ouput.txt
```

**Example Usage:**

`unshadow local_passwd local_shadow > unshadowed.txt`

## **Cracking**

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```
