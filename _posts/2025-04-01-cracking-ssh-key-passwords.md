---
title: "Cracking SSH Key Passwords"
date: 2025-04-01 14:30:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "using John to crack the SSH private key password of id_rsa files. Unless configured otherwise, you authenticate your SSH login using a password. However, you…"
media_subpath: /assets/img/tryhackme/2025-04-01-cracking-ssh-key-passwords/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/cracking-ssh-key-passwords/
th_id: "cyber-101/cryptography-basics/john-the-ripper/cracking-ssh-key-passwords"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 7
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

using John to crack the SSH private key password of `id_rsa` files. Unless configured otherwise, you authenticate your SSH login using a password. However, you can configure key-based authentication, which lets you use your private key, `id_rsa`, as an authentication key to log in to a remote machine over SSH. However, doing so will often require a password to access the private key; here, we will be using John to crack this password to allow authentication over SSH using the key.

## **SSH2John**

 `ssh2john` converts the `id_rsa` private key, which is used to log in to the SSH session, into a hash format that John can work with. 

```bash
ssh2john [id_rsa private key file] > [output file]
```

Note that if you don’t have `ssh2john` installed, you can use `ssh2john.py`

## **Cracking**

For the final time, we’re feeding the file we output from ssh2john, which in our example use case is called `id_rsa_hash.txt` and, as we did with `rar2john`, we can use this seamlessly with John:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```
