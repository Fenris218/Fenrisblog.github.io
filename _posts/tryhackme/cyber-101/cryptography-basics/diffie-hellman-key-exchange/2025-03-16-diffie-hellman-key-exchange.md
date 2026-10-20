---
title: "Diffie-Hellman Key Exchange"
date: 2025-03-16 10:14:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "DH cho phép hai người tạo ra cùng một khóa bí mật, mà không ai thực sự gửi khóa đó đi."
media_subpath: /assets/img/tryhackme/2025-03-16-diffie-hellman-key-exchange/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/diffie-hellman-key-exchange/
th_id: "cyber-101/cryptography-basics/diffie-hellman-key-exchange"
th_parent: "cyber-101/cryptography-basics"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics"]
---

{% include tryhackme-nav.html %}

### 🔑 Ý tưởng chính của Diffie–Hellman

DH cho phép **hai người tạo ra cùng một khóa bí mật**, **mà không ai thực sự gửi khóa đó đi**.

---

### 💡 Mô phỏng bằng ví dụ “pha màu sơn”

1. Cả hai cùng **chọn một màu chung** (public) — ví dụ màu vàng → gọi là **C**.
2. Alice chọn **màu bí mật riêng A** (private secret).
    
    Bob chọn **màu bí mật riêng B**.
    
3. Họ **trộn** màu riêng của mình với màu chung:
    - Alice tạo **AC** (vàng + bí mật của cô ấy)
    - Bob tạo **BC** (vàng + bí mật của anh ấy)
4. Họ **gửi cho nhau** bản pha trộn đó (AC và BC).
    
    Ai nhìn vào cũng chỉ thấy “màu pha”, **không biết được màu bí mật** (vì tách màu rất khó).
    
5. Bây giờ, mỗi người **trộn thêm màu riêng của mình** vào phần nhận được:
    - Alice lấy **BC** từ Bob và trộn thêm **A** → tạo **ABC**
    - Bob lấy **AC** từ Alice và trộn thêm **B** → tạo **ABC**

👉 Kết quả: **cả hai cùng có chung một “màu bí mật” (ABC)**,

nhưng **không ai gửi màu đó đi trực tiếp** qua mạng.

---

### 🔐 Trong toán học thật (phiên bản số học)

- Chọn số nguyên lớn ppp (prime) và số ggg (generator) — đều **công khai**.
- Alice chọn bí mật aaa, tính A=gamod  pA = g^a \mod pA=gamodp, gửi A cho Bob.
- Bob chọn bí mật bbb, tính B=gbmod  pB = g^b \mod pB=gbmodp, gửi B cho Alice.
- Sau đó:
    - Alice tính K=Bamod  p=gbamod  pK = B^a \mod p = g^{ba} \mod pK=Bamodp=gbamodp
    - Bob tính K=Abmod  p=gabmod  pK = A^b \mod p = g^{ab} \mod pK=Abmodp=gabmodp

→ Kết quả: **Alice và Bob có cùng một khóa K = g^{ab} mod p**,

mà người nghe lén chỉ thấy gag^aga và gbg^bgb – **rất khó đảo ngược để tìm a hoặc b**.

---

### ✅ Tóm lại

Diffie–Hellman cho phép hai bên:

- Tạo ra một **khóa bí mật chung**,
- Mà **không phải gửi khóa đó qua mạng**,
- Nhờ vào **toán học một chiều (modular exponentiation)** – dễ làm một chiều, khó làm ngược.

---

Nếu bạn muốn, mình có thể minh họa bằng **một ví dụ số cụ thể (với p, g, a, b)** để bạn thấy rõ từng bước tính ra cùng một khóa. Bạn có muốn mình làm ví dụ đó không?
