---
title: "Tunneling"
date: 2025-01-30 13:29:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "In networking, tunnels are a method for transporting data across a network using protocols that are not supported by that network. Tunneling works by encapsu…"
media_subpath: /assets/img/tryhackme/2025-01-30-tunneling/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/tunneling/
th_id: "cyber-101/network/tunneling"
th_parent: "cyber-101/network"
th_kind: note
th_order: 17
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/network"]
---

{% include tryhackme-nav.html %}

## What is tunneling

In networking, tunnels are a method for transporting data across a network using [protocols](https://www.cloudflare.com/learning/network-layer/what-is-a-protocol/) that are not supported by that network. Tunneling works by encapsulating packets: wrapping packets inside of other packts.

## **How does packet encapsulation work?**

Data traveling over a network is divided into packets. A typical packet has two parts: the header, which indicates the packet's destination and which protocol it uses, and the payload, which is the packet's actual contents.

An encapsulated packet is essentially a packet inside another packet. In an encapsulated packet, the header and payload of the first packet goes inside the payload section of the surrounding packet. The original packet itself becomes the payload.

## **Why is encapsulation useful?**

Encapsulation is also useful for encrypted network connections.  If a packet is completely encrypted, including the header, then network routers will not be able to forward the packet to its destination since they do not have the key and cannot see its header. By wrapping the encrypted packet inside another unencrypted packet, the packet can travel across networks like normal.
