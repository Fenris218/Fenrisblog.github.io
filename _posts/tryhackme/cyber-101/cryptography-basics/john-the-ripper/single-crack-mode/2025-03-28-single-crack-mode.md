---
title: "Single crack mode"
date: 2025-03-28 10:26:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "John cần file chứa hash theo các định dạng chuẩn (ví dụ /etc/shadow-style hoặc user:hash). Chế độ Single đọc username trong file để sinh mật khẩu"
media_subpath: /assets/img/tryhackme/2025-03-28-single-crack-mode/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/john-the-ripper/single-crack-mode/
th_id: "cyber-101/cryptography-basics/john-the-ripper/single-crack-mode"
th_parent: "cyber-101/cryptography-basics/john-the-ripper"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/john-the-ripper"]
---

{% include tryhackme-nav.html %}

## Chế độ Single là gì

- **Mục tiêu:** Tạo mật khẩu thử nghiệm **từ thông tin tài khoản** (chủ yếu là username và các trường GECOS) thay vì dùng wordlist ngoài.
- **Cách hoạt động:** John áp dụng các quy tắc biến đổi heuristic lên username (cắt, đổi hoa/thường, thêm số, thay thế kiểu leetspeak, đảo chuỗi, tách camelCase…) để sinh ra candidates.
- **Khi nào dùng:** Khi nghi tài khoản dùng mật khẩu dễ đoán dựa trên username hoặc tên thật (ví dụ `john123`, `John2020`, `doe1987`, `jdoe!`).

## Định dạng input

John cần file chứa hash theo các định dạng chuẩn (ví dụ `/etc/shadow`-style hoặc `user:hash`). Chế độ Single đọc username trong file để sinh mật khẩu

## **Using Single Crack Mode**

To use single crack mode, we use roughly the same syntax that we’ve used so far; for example, if we wanted to crack the password of the user named “Mike”, using the single mode, we’d use:

`john --single --format=[format] [path to file]`

- `-single`: This flag lets John know you want to use the single hash-cracking mode
- `-format=[format]`: As always, it is vital to identify the proper format.

**Example Usage:**

`john --single --format=raw-sha256 hashes.txt`

**A Note on File Formats in Single Crack Mode:**

If you’re cracking hashes in single crack mode, you need to change the file format that you’re feeding John for it to understand what data to create a wordlist from. You do this by prepending the hash with the username that the hash belongs to, so according to the above example, we would change the file `hashes.txt`

**From** `1efee03cdcb96d90ad48ccc7b8666033`

**To** `mike:1efee03cdcb96d90ad48ccc7b8666033`
