---
title: "Shell Payloads"
date: 2025-04-30 19:59:00 +0700
categories: ["TryHackMe", "Cyber 101", "Offensive Security Tooling"]
tags: ["tryhackme", "offensive-security-tooling"]
description: "👉 Descriptor là con số đại diện cho luồng dữ liệu mà chương trình dùng để đọc / ghi."
media_subpath: /assets/img/tryhackme/2025-04-30-shell-payloads/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/offensive-security-tooling/shell/shell-payloads/
th_id: "cyber-101/offensive-security-tooling/shell/shell-payloads"
th_parent: "cyber-101/offensive-security-tooling/shell"
th_kind: note
th_order: 4
th_course: "cyber-101"
th_module: "cyber-101/offensive-security-tooling"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/offensive-security-tooling", "cyber-101/offensive-security-tooling/shell"]
---

{% include tryhackme-nav.html %}

## Descriptor

### 1️⃣ Descriptor (File Descriptor) là gì?

👉 **Descriptor** là **con số đại diện cho luồng dữ liệu** mà chương trình dùng để **đọc / ghi**.

#### 3 descriptor mặc định:

| FD | Tên | Chức năng |
| --- | --- | --- |
| `0` | stdin | Input |
| `1` | stdout | Output |
| `2` | stderr | Error |

📌 Ngoài ra có thể có FD `3,4,5,...` (file, pipe, socket…)

### 2️⃣ Redirect descriptor là gì?

👉 **Redirect descriptor** = **chuyển hướng luồng dữ liệu của descriptor sang nơi khác**

### 3️⃣ Ký hiệu cơ bản cần nhớ

#### Output (`>`)

```bash
ls > out.txt
```

- stdout → file

#### Input (`<`)

```bash
cat < in.txt
```

- stdin ← file

### 4️⃣ Redirect error

```bash
ls not_exist 2> err.txt

```

- stderr → file

---

### 5️⃣ Redirect giữa các descriptor

| Cú pháp | Nghĩa |
| --- | --- |
| `2>&1` | stderr → stdout |
| `1>&2` | stdout → stderr |
