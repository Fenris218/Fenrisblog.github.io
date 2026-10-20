---
title: "Window Fundamental"
date: 2025-01-02 09:01:00 +0700
categories: ["TryHackMe", "Cyber 101", "Window Fundamental"]
tags: ["tryhackme", "window-fundamental"]
description: "Ví dụ : Giả sử bạn có một tệp example.txt."
media_subpath: /assets/img/tryhackme/2025-01-02-window-fundamental/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/window-fundamental/
th_id: "cyber-101/window-fundamental"
th_parent: "cyber-101"
th_kind: module
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/window-fundamental"
th_size: 5
th_ancestors: ["cyber-101"]
---

{% include tryhackme-nav.html %}

- ADS : là một **tính năng của hệ thống tập tin NTFS** trong Windows, cho phép **một tệp có thể chứa nhiều luồng dữ liệu ($DATA)** khác nhau, mà **Windows Explorer không hiển thị** cho người dùng.

Ví dụ :  Giả sử bạn có một tệp `example.txt`.

Bạn có thể tạo thêm một luồng dữ liệu ẩn bằng PowerShell hoặc Command Prompt:

```bash
echo "Hello from ADS!" > example.txt:hidden

```

Tệp `example.txt` vẫn hiển thị dung lượng như cũ, nhưng thực tế nó đang chứa thêm dữ liệu ẩn trong luồng `hidden`.

Để đọc lại luồng ẩn này:

```bash
more < example.txt:hidden

```

- *Microsoft Defender SmartScreen:*  **ngăn người dùng truy cập hoặc tải về nội dung nguy hiểm từ Internet**.
    - chống trang web lừa đảo (Phishing)
    - Kiểm tra file tải xuống
- 

[**Active Directory Basics**]({{ site.baseurl }}/tryhackme/cyber-101/window-fundamental/active-directory-basics/)

[Powershell]({{ site.baseurl }}/tryhackme/cyber-101/window-fundamental/powershell/)
