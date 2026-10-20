---
title: "Cracking Basic Hashes"
date: 2025-03-26 08:24:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "John Basic Syntax :"
media_subpath: /assets/img/tryhackme/2025-03-26-cracking-basic-hashes/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/cracking-basic-hashes/
th_id: "cyber-101/cryptography-basics/john-the-ripper/cracking-basic-hashes"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

**John Basic Syntax :** 

```bash
john [options] [file path]
```

**Automatic Cracking**

 if you can’t identify what hash type you’re working with and want to try cracking it, it can be a good option! To do this, we use the following syntax:

`john --wordlist=[path to wordlist] [path to file]`

Ví dụ ;

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

## **Format-Specific Cracking**

Once you have identified the hash that you’re dealing with, you can tell John to use it while cracking the provided hash using the following syntax:

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

**Example Usage:**

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

**A Note on Formats:**

When you tell John to use formats, if you’re dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with `raw-` to tell John you’re just dealing with a standard hash type, though this doesn’t always apply. To check if you need to add the prefix or not, you can list all of John’s formats using `john --list=formats` and either check manually or grep for your hash type using something like `john --list=formats | grep -iF "md5"`.
