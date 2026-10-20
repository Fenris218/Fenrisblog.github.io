---
title: "Identifying Hosts: DHCP, NetBIOS, Kerberos"
date: 2025-02-21 11:51:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "When investigating a compromise or malware infection activity, a security analyst should know how to identify the hosts on the network apart from IP to MAC a…"
media_subpath: /assets/img/tryhackme/2025-02-21-identifying-hosts-dhcp-netbios-kerberos/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/identifying-hosts-dhcp-netbios-kerberos/
th_id: "cyber-101/wireshark/identifying-hosts-dhcp-netbios-kerberos"
th_parent: "cyber-101/wireshark"
th_kind: note
th_order: 11
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark"]
---

{% include tryhackme-nav.html %}

When investigating a compromise or malware infection activity, a security analyst should know how to identify the hosts on the network apart from IP to MAC address match. One of the best methods is identifying the hosts and users on the network to decide the investigation's starting point and list the hosts and users associated with the malicious traffic/activity.

Usually, enterprise networks use a predefined pattern to name users and hosts. While this makes knowing and following the inventory easier, it has good and bad sides. The good side is that it will be easy to identify a user or host by looking at the name. The bad side is that it will be easy to clone that pattern and live in the enterprise network for adversaries. There are multiple solutions to avoid these kinds of activities, but for a security analyst, it is still essential to have host and user identification skills.

Protocols that can be used in Host and User identification:

- Dynamic Host Configuration Protocol (DHCP) traffic
- NetBIOS (NBNS) traffic
- Kerberos traffic

## DHCP

| **Notes** | **Wireshark Filter** |
| --- | --- |
| Global search. | • `dhcp`or`bootp` |
| • **"DHCP Request"**packets contain the hostname information<br>• **"DHCP ACK"**packets represent the accepted requests<br>• **"DHCP NAK"**packets represent denied requests<br>Due to the nature of the protocol, only "Option 53" ( request type) has predefined static values. You should filter the packet type first, and then you can filter the rest of the options by "applying as column" or use the advanced filters like "contains" and "matches". | • Request: `dhcp.option.dhcp == 3`<br>• ACK: `dhcp.option.dhcp == 5`<br>• NAK: `dhcp.option.dhcp == 6` |
| **"DHCP Request"**options for grabbing the low-hanging fruits:<br>• **Option 12:**Hostname.<br>• **Option 50:**Requested IP address.<br>• **Option 51:**Requested IP lease time.<br>• **Option 61:**Client's MAC address. | • `dhcp.option.hostname contains "keyword"` |
| **"DHCP ACK"**options for grabbing the low-hanging fruits:<br>• **Option 15:**Domain name.<br>• **Option 51:**Assigned IP lease time. | • `dhcp.option.domain_name contains "keyword"` |
| **"DHCP NAK"**options for grabbing the low-hanging fruits:<br>• **Option 56:**Message (rejection details/reason). | As the message could be unique according to the case/situation, It is suggested to read the message instead of filtering it. Thus, the analyst could create a more reliable hypothesis/result by understanding the event circumstances. |

## **NetBIOS (NBNS) Analysis**

**NetBIOS** or **Net**work **B**asic **I**nput/**O**utput **S**ystem is the technology responsible for allowing applications on different hosts to communicate with each other. 

Nó phổ biến trong hệ thống Windows đời cũ trước khi DNS được dùng rộng rãi.

| **Notes** | **Wireshark Filter** |
| --- | --- |
| Global search. | • `nbns` |
| **"NBNS"** options for grabbing the low-hanging fruits:<br>• **Queries:**Query details.<br>• Query details could contain **"name, Time to live (TTL) and IP address details"** | • `nbns.name contains "keyword"` |

## **Kerberos Analysis**

**Kerberos** is the default authentication service for Microsoft Windows domains. It is responsible for authenticating service requests between two or more computers over the untrusted network. The ultimate aim is to prove identity securely.

| **Notes** | **Wireshark Filter** |
| --- | --- |
| Global search. | • `kerberos` |
| User account search:<br>• **CNameString:**The username.<br>**Note:** Some packets could provide hostname information in this field. To avoid this confusion, filter the **"$"**value. The values end with**"$"**are hostnames, and the ones without it are user names. | • `kerberos.CNameString contains "keyword"`<br>• `kerberos.CNameString and !(kerberos.CNameString contains "$" )` |
| "Kerberos" options for grabbing the low-hanging fruits:<br>• **pvno:**Protocol version.<br>• **realm:**Domain name for the generated ticket.<br>• **sname:**Service and domain name for the generated ticket.<br>• **addresses:**Client IP address and NetBIOS name.<br>**Note: the "addresses" information is only available in request packets.** | • `kerberos.pvno == 5`<br>• `kerberos.realm contains ".org"`<br>• `kerberos.SNameString == "krbtg"` |

### 🔹 Kerberos flow tổng thể (3 bước chính)

Trong hệ thống như Active Directory:

#### 1️⃣ AS-REQ / AS-REP

→ Xin **TGT (Ticket Granting Ticket)**

👉 Chứng minh bạn là ai.

#### 2️⃣ TGS-REQ / TGS-REP

→ Xin **Service Ticket**

👉 Xin quyền truy cập dịch vụ cụ thể.

#### 3️⃣ AP-REQ / AP-REP

→ Gửi ticket cho server để vào dịch vụ.
