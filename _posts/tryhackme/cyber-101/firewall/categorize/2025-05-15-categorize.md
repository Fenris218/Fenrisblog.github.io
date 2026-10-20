---
title: "Categorize"
date: 2025-05-15 10:14:00 +0700
categories: ["TryHackMe", "Cyber 101", "Firewall"]
tags: ["tryhackme", "firewall"]
description: "Firewalls are categorized into many types."
media_subpath: /assets/img/tryhackme/2025-05-15-categorize/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/firewall/categorize/
th_id: "cyber-101/firewall/categorize"
th_parent: "cyber-101/firewall"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/firewall"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/firewall"]
---

{% include tryhackme-nav.html %}

Firewalls are categorized into many types. 

## **Stateless Firewall**

operates on layer 3 and layer 4 of the OSI model. It will match every packet with the rules regardless of whether it is part of a legitimate connection. It maintains no information on the state of the previous connections to make decisions for future packets. Due to this, these firewalls can process the packets quickly. However, they cannot apply complex policies to the data based on its relationship with the previous connections. 

Suppose the firewall denies a few packets from a single source based on its rules. Ideally, it should drop all the future packets from this source because the previous packets could not comply with the firewall’s rules. However, the firewall keeps forgetting this, and future packets from this source will be treated as new and matched by its rules again.

## **Stateful Firewall**

Stateful firewalls operate at layer 3 and layer 4 of the OSI model. This type of firewall goes beyond filtering packets by predetermined rules. It also keeps track of previous connections and stores them in a state table. Suppose the firewall accepts a few packets from a source address based on its rules. In that case, it will take note of this connection in its stated table and allow all the future packets for this connection to automatically get allowed without inspecting each of them. Similarly, the stateful firewalls take note of the connections for which they deny a few packets, and based upon this information, they deny all the subsequent packets coming from the same source.

## **Proxy Firewall**

operate on the OSI model’s layer 7. The problem with previous firewalls was their inability to inspect the contents of a packet. Proxy firewalls, or application-level gateways, act as intermediaries between the private network and the Internet and operate on the OSI model’s layer 7. They inspect the content of all packets as well. The requests made by users in a network are forwarded by this proxy after inspection and masking them with their own IP address to provide anonymity for the internal IP addresses. Content filtering policies can be applied to these firewalls to allow/deny incoming and outgoing traffic based on their content.

## **Next-Generation Firewall (NGFW)**

This is the most advanced type of firewall that operates from layer 3 to layer 7 of the OSI model. Offering deep packet inspection and other functionalities that enhance the security of incoming and outgoing network traffic. It has an intrusion prevention system that blocks malicious activities in real time.

| **Firewalls** | **Characteristics** |
| --- | --- |
| Stateless firewalls | - Basic filtering- No track of previous connections- Efficient for high-speed networks |
| Stateful firewalls | - Recognize traffic by patterns- Complex rules can be applicable- Monitor the network connections |
| Proxy firewalls | - Inspect the data inside the packets as well- Provides content filtering options- Provides application control- Decrypts and inspects SSL/TLS data packets |
| Next-generation firewalls | - Provides advanced threat protection- Comes with an intrusion prevention system- Identify anomalies based on heuristic analysis- Decrypts and inspects SSL/TLS data packets |
