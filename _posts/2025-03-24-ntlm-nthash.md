---
title: "NTLM/NTHASH"
date: 2025-03-24 18:22:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "NThash is the hash format modern Windows operating system machines use to store user and service passwords. It’s also commonly referred to as NTLM- đó là dạn…"
media_subpath: /assets/img/tryhackme/2025-03-24-ntlm-nthash/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/hash/ntlm-nthash/
th_id: "cyber-101/cryptography-basics/hash/ntlm-nthash"
th_parent: "cyber-101/cryptography-basics/hash"
th_kind: note
th_order: 4
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/hash"]
---

{% include tryhackme-nav.html %}

NThash is the hash format modern Windows operating system machines use to store user and service passwords. It’s also commonly referred to as NTLM- đó là dạng hash không dùng salt, nên dễ bị tấn công bằng dictionary/rainbow nếu mật khẩu yếu..

In Windows, SAM (Security Account Manager) is used to store user account information, including usernames and hashed passwords. You can acquire NTHash/NTLM hashes by dumping the SAM database on a Windows machine, using a tool like Mimikatz, or using the Active Directory database: `NTDS.dit`. You may not have to crack the hash to continue privilege escalation, as you can often conduct a “pass the hash” attack instead, but sometimes, hash cracking is a viable option if there is a weak password policy.

### “Pass the Hash” là gì — tại sao không cần crack?

- **Pass-the-hash (PtH)**: thay vì biết mật khẩu plaintext, kẻ tấn công dùng trực tiếp hash (NTLM) để xác thực với các dịch vụ/host khác — các giao thức Windows cho phép sử dụng credential dạng hash trong nhiều tình huống.
- Vì vậy, nếu kẻ tấn công có hash, họ **thường không cần** crack để leo thang đặc quyền — chỉ reuse hash để di chuyển trong mạng.
