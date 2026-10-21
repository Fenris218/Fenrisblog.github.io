---
title: "Powershell"
date: 2025-01-06 13:05:00 +0700
categories: ["TryHackMe", "Cyber 101", "Window Fundamental"]
tags: ["tryhackme", "window-fundamental"]
description: "Powershell ability"
media_subpath: /assets/img/tryhackme/2025-01-06-powershell/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/window-fundamental/powershell/
th_id: "cyber-101/window-fundamental/powershell"
th_parent: "cyber-101/window-fundamental"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/window-fundamental"
th_size: 1
th_ancestors: ["cyber-101", "cyber-101/window-fundamental"]
---

{% include tryhackme-nav.html %}

Powershell ability

- Powershell xử lý dữ liệu dạng Object thay vì text như CMD nên có thể dễ dàng truy cập thuộc tính và phương thức của Object ( thứ mà CMD ko làm được )

## 🧩 1. Trong **Command Prompt (cmd)**

- Mọi thứ chỉ là **văn bản (text)**.
- Khi bạn chạy một lệnh, kết quả chỉ là **chuỗi chữ** hiển thị ra màn hình.
- Muốn lấy thông tin cụ thể (ví dụ tên file, kích thước...) bạn phải **tự tách chuỗi bằng tay**.

👉 Ví dụ: dir

kết quả là:

```
01/11/2025  08:00 AM    <DIR>          Documents
01/11/2025  08:01 AM             1,024 test.txt

```

Muốn lấy riêng “test.txt” → bạn phải tự phân tích chuỗi (rất thủ công).

---

## ⚙️ 2. Trong **PowerShell**

- Mọi thứ là **đối tượng (object)** chứ không chỉ là text.
- Khi bạn chạy một lệnh (cmdlet), nó trả về **object có thuộc tính (property)** và **phương thức (method)**.

👉 Ví dụ:

```
Get-ChildItem
```

trả về **các đối tượng file và thư mục**.

Mỗi object có nhiều **thuộc tính**, ví dụ:

- `.Name` → tên file
- `.Length` → kích thước
- `.LastWriteTime` → thời gian sửa đổi cuối

---

## 💡 Ví dụ cụ thể

### Trong CMD:

```
dir | find "txt"

```

→ chỉ lọc văn bản, không hiểu file là gì, chỉ lọc dòng có “txt”.

### Trong PowerShell:

```
Get-ChildItem | Where-Object {$_.Extension -eq ".txt"}
```

→ hiểu rõ từng file là **object** có thuộc tính `.Extension` nên lọc chính xác các file `.txt`.

---

## 🧠 3. “Không cần parse text nữa”

Vì PowerShell trả về **object có cấu trúc sẵn**, bạn không phải “phân tích chuỗi” thủ công nữa.

Ví dụ:

```
$process = Get-Process notepad
$process.Kill()
```

Ở đây:

- `$process` là object chứa thông tin về tiến trình Notepad.
- `.Kill()` là **method (hàm)** của object, giúp dừng tiến trình ngay.

Trong CMD, bạn phải dùng:

```
taskkill /IM notepad.exe /F
```

→ chỉ dựa vào text, không có khái niệm object hay method.

