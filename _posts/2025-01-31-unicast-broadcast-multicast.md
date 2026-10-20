---
title: "Unicast-Broadcast-Multicast"
date: 2025-01-31 14:30:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "👉 IP multicast nằm giữa unicast và broadcast:"
media_subpath: /assets/img/tryhackme/2025-01-31-unicast-broadcast-multicast/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/unicast-broadcast-multicast/
th_id: "cyber-101/network/unicast-broadcast-multicast"
th_parent: "cyber-101/network"
th_kind: note
th_order: 18
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/network"]
---

{% include tryhackme-nav.html %}

#### ✅ **Unicast**

- 1 → 1
- Ví dụ: bạn gửi email cho một người.

#### ✅ **Broadcast**

- 1 → tất cả trong mạng
- Ví dụ: ARP request.

#### ✅ **Multicast**

- 1 → nhiều người **được chọn trước**
- Ví dụ: livestream, IPTV.

👉 IP multicast nằm giữa unicast và broadcast:

- Không gửi cho tất cả.
- Chỉ gửi cho nhóm quan tâm.

### 🔹 2. Ví dụ thực tế

Ví dụ một server livestream:

- 1000 người xem cùng lúc.
- Nếu dùng **unicast** → server phải gửi 1000 bản dữ liệu.
- Nếu dùng **multicast** → server chỉ gửi **1 bản**, router sẽ nhân bản khi cần.

➡️ Tiết kiệm băng thông rất nhiều.

### 🔹 3. Cách hoạt động

Multicast dựa trên:

- **Group (nhóm multicast)**
- Thiết bị muốn nhận phải “join group”.

Các bước:

1. Server gửi dữ liệu đến địa chỉ multicast.
2. Client đăng ký tham gia nhóm.
3. Router chỉ forward dữ liệu đến nơi có người đăng ký.

### 🔹 4. Địa chỉ IP multicast

Trong IPv4:

- Từ **224.0.0.0 → 239.255.255.255 ( IP của group join multicast)**

Ví dụ:

- 224.x.x.x: multicast.

Một số nhóm phổ biến:

- 224.0.0.1: tất cả host trong mạng.

## 🔹 IGMP Join là gì?

**Internet Group Management Protocol (IGMP)** là giao thức dùng để:

> Cho host thông báo với router rằng nó muốn tham gia (join) một multicast group.
> 

⇒ muốn biết ai nhận tin gói tin gửi đến multicast thì xem IGMP join
