---
title: "Asymmetric"
date: 2025-03-14 08:12:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "Mỗi bên có cặp khóa : public key (công khai) và private key (bí mật)."
media_subpath: /assets/img/tryhackme/2025-03-14-asymmetric/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/types-of-encryption/asymmetric/
th_id: "cyber-101/cryptography-basics/types-of-encryption/asymmetric"
th_parent: "cyber-101/cryptography-basics/types-of-encryption"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 1
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/types-of-encryption"]
---

{% include tryhackme-nav.html %}

Mỗi bên có **cặp khóa** : public key (công khai) và private key (bí mật).

➜ Mã hóa bằng public key thì chỉ có private key tương ứng mới giải mã được.

➜ Nhưng kiểu mã hóa này **rất chậm**, nên chỉ dùng trong giai đoạn “trao đổi khóa”.

![image.png](image.png)

[Thuật toán RSA]({{ site.baseurl }}/tryhackme/cyber-101/cryptography-basics/types-of-encryption/asymmetric/thuat-toan-rsa/)
