---
title: "Types of Encryption"
date: 2025-03-13 19:11:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "Symmetric encryption, also known as symmetric cryptography, uses the same key to encrypt and decrypt the data Examples of symmetric encryption are DES (Data…"
media_subpath: /assets/img/tryhackme/2025-03-13-types-of-encryption/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/types-of-encryption/
th_id: "cyber-101/cryptography-basics/types-of-encryption"
th_parent: "cyber-101/cryptography-basics"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 2
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics"]
---

{% include tryhackme-nav.html %}

Symmetric **encryption**, also known as **symmetric cryptography**, uses the same key to encrypt and decrypt the data
Examples of symmetric encryption are DES (Data Encryption Standard), 3DES (Triple DES) and AES (Advanced Encryption Standard).

[Asymmetric ]({{ site.baseurl }}/tryhackme/cyber-101/cryptography-basics/types-of-encryption/asymmetric/)

 Unlike symmetric encryption, which uses the same key for encryption and  decryption, asymmetric **encryption** uses a pair of keys, one to encrypt and the other to decrypt. Examples are RSA, Diffie-Hellman, and Elliptic Curve cryptography (ECC). The two keys involved in the process are referred to as a **public key** and a **private key**.

Asymmetric encryption tends to be slower, and many asymmetric encryption ciphers use larger keys than symmetric encryption. For example, RSA uses 2048-bit, 3072-bit, and 4096-bit keys; 2048-bit is the recommended minimum key size. Diffie-Hellman also has a recommended minimum key size of 2048 bits but uses 3072-bit and 4096-bit keys for enhanced security. On the other hand, ECC can achieve equivalent security with shorter keys. For example, with a 256-bit key, ECC provides a level of security comparable to a 3072-bit RSA key.
