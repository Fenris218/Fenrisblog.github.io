---
title: "SSL stripping"
date: 2025-01-25 08:24:00 +0700
categories: ["TryHackMe", "Cyber 101", "Network"]
tags: ["tryhackme", "network"]
description: "SSL stripping is a man-in-the-middle technique in which an attacker intercepts and modifies traffic to remove or prevent TLS encryption between a client and…"
media_subpath: /assets/img/tryhackme/2025-01-25-ssl-stripping/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/network/tls/ssl-stripping/
th_id: "cyber-101/network/tls/ssl-stripping"
th_parent: "cyber-101/network/tls"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/network"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/network", "cyber-101/network/tls"]
---

{% include tryhackme-nav.html %}

SSL stripping is a man-in-the-middle technique in which an attacker intercepts and modifies traffic to remove or prevent TLS encryption between a client and a server. This causes the client to communicate over HTTP instead of HTTPS.

## **How It Works**

1. **The victim initiates an HTTPS request** to a website.
2. **The attacker intercepts the request** using ARP spoofing or a rogue access point.
3. **The attacker connects to the website over HTTPS** but relays the response to the victim through HTTP
4. **The victim unknowingly interacts over HTTP**, exposing sensitive data in plaintext.

## **Indicators of SSL stripping**

- **Initial Request vs. Response:** The user's initial request may be for `HTTPS` (port 443), but the subsequent packets immediately shift to unencrypted `HTTP` (port 80) for the same domain.
- **Redirects/Link Rewriting**: Monitoring for redirects ( Status Codes 301, 302) that persistently direct an HTTPS request to an HTTP resource.
- **Certificate Errors**: Although the attacker usually tries to hide this, the initial **TLS/SSL Handshake** may fail or display a self-signed certificate if the attacker uses a more direct proxying technique.

https://tryhackme.com/room/mitmdetection?taskNo=6&sharerId=6704a924d9503f79da2f5690
