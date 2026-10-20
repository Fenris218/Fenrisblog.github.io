---
title: "Cracking a Password-Protected RAR Archive"
date: 2025-03-31 13:29:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "Almost identical to the zip2john tool, we will use the rar2john tool to convert the RAR file into a hash format that John can understand. The basic syntax is…"
media_subpath: /assets/img/tryhackme/2025-03-31-cracking-a-password-protected-rar-archive/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/cracking-a-password-protected-rar-archive/
th_id: "cyber-101/cryptography-basics/john-the-ripper/cracking-a-password-protected-rar-archive"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 6
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

## **Rar2John**

Almost identical to the `zip2john` tool, we will use the `rar2john` tool to convert the RAR file into a hash format that John can understand. The basic syntax is as follows:

```bash
rar2john [rar file] > [output file]
```

**Example Usage**

`/opt/john/rar2john rarfile.rar > rar_hash.txt`

## **Cracking**

Once again, we can take the file we output from `rar2john` in our example use case, `rar_hash.txt`, and feed it directly into John as we did with `zip2john`.

`john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt`
