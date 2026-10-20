---
title: "Cracking Password Protected Zip Files"
date: 2025-03-30 12:28:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "we’ll use a separate part of the John suite of tools to convert the Zip file into a format that John will understand, but we’ll use the syntax you’re already…"
media_subpath: /assets/img/tryhackme/2025-03-30-cracking-password-protected-zip-files/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/cracking-password-protected-zip-files/
th_id: "cyber-101/cryptography-basics/john-the-ripper/cracking-password-protected-zip-files"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 5
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

we’ll use a separate part of the John suite of tools to convert the Zip file into a format that John will understand, but we’ll use the syntax you’re already familiar with for all intents and purposes.

**Zip2John**

 we will use the `zip2john` tool to convert the Zip file into a hash format that John can understand and hopefully crack. 

```bash
zip2john [options] [zip file] > [output file]
```

`[options]`: Allows you to pass specific checksum options to `zip2john`; this shouldn’t often be necessary

**Cracking**

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```
