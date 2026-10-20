---
title: "PGP and GPG"
date: 2025-03-19 13:17:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "PGP (viết tắt của *Pretty Good Privacy*) là một phần mềm sử dụng kỹ thuật mã hóa (encryption) để:"
media_subpath: /assets/img/tryhackme/2025-03-19-pgp-and-gpg/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/pgp-and-gpg/
th_id: "cyber-101/cryptography-basics/pgp-and-gpg"
th_parent: "cyber-101/cryptography-basics"
th_kind: note
th_order: 5
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics"]
---

{% include tryhackme-nav.html %}

**PGP** (viết tắt của *Pretty Good Privacy*) là một phần mềm sử dụng kỹ thuật **mã hóa (encryption)** để:

- Mã hóa file (giữ bí mật dữ liệu)
- Ký số (digital signing) để xác thực người gửi và đảm bảo tính toàn vẹn của dữ liệu
- Và còn có nhiều ứng dụng khác

**GnuPG (hoặc GPG)** là phiên bản **mã nguồn mở** của tiêu chuẩn **OpenPGP** — một chuẩn mở được phát triển từ PGP để mọi người có thể dùng mà không cần phần mềm thương mại.

**GPG thường được dùng trong email để**:

- **Bảo mật nội dung email** (chỉ người nhận hợp lệ mới đọc được)
- **Ký điện tử email**, giúp xác minh email thực sự do người gửi đó gửi, và **nội dung không bị sửa đổi**.

Below is an example of generating GPG. You are asked about the purpose of using `gpg`, whether signing only or signing and encrypting. Besides selecting the cryptographic algorithm, we needed to choose an expiry date for the generated key. Finally, we provided some information about us: our name, email address, and a comment usually about the purpose of this key.

```bash
gpg --full-gen-key
gpg (GnuPG) 2.4.4; Copyright (C) 2024 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 9
Please select which elliptic curve you want:
   (1) Curve 25519 *default*
   (4) NIST P-384
   (6) Brainpool P-256
Your selection? 1
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: strategos
Email address: strategos@tryhackme.thm
[...]
pub   ed25519 2024-08-29 [SC]
      AB7E6AA87B6A8E0D159CA7FFE5E63DBD5F83D5ED
uid                      Strategos <strategos@tryhackme.thm>
sub   cv25519 2024-08-29 [E]
```
