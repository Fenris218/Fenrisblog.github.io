---
title: "Evasion via Controlling the Source MAC/IP/PORT"
date: 2025-06-02 16:32:00 +0700
categories: ["TryHackMe", "Cyber 101", "Firewall"]
tags: ["tryhackme", "firewall"]
description: "When scanning a host behind a firewall, the firewall will usually detect and block port scans. This situation would require you to adapt your network and por…"
media_subpath: /assets/img/tryhackme/2025-06-02-evasion-via-controlling-the-source-mac-ip-port/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/firewall-2/evasion-via-controlling-the-source-mac-ip-port/
th_id: "cyber-101/firewall-2/evasion-via-controlling-the-source-mac-ip-port"
th_parent: "cyber-101/firewall-2"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/firewall-2"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/firewall-2"]
---

{% include tryhackme-nav.html %}

When scanning a host behind a firewall, the firewall will usually detect and block port scans. This situation would require you to adapt your network and port scan to trốn tránh the firewall. A network scanner like Nmap provides few features to help with such a task. 

Nmap allows you to hide or spoof the source as you can use:

1. Decoy(s)
2. Proxy
3. Spoofed MAC Address
4. Spoofed Source IP Address
5. Fixed Source Port Number

## 1. Decoy(s)

Using decoys makes your IP address mix with other “decoy” IP addresses. Consequently, it will be difficult for the firewall and target host to know where the port scan is coming from. Moreover, this can exhaust the blue team investigating each source IP address.

Using the `-D` option, you can add decoy source IP addresses to confuse the target. Consider the following command, `nmap -sS -Pn -D 10.10.10.1,10.10.10.2,ME -F MACHINE_IP`. The Wireshark capture is shown in the following figure.

![image.png](image.png)

The target `MACHINE_IP` will also see scans coming from `10.10.10.1` and `10.10.10.2` when only one source IP address, `ME`, is running the scan. Note that if you omit the `ME` entry in the scan command, Nmap will put your real IP address, i.e. `ME`, in a random position.

You can also set Nmap to use random source IP addresses instead of explicitly specifying them. By running `nmap -sS -Pn -D RND,RND,ME -F MACHINE_IP`, Nmap will choose two random source IP addresses to use as decoys.

## 2. Proxy

This technique allows you to keep your IP address hidden while the target logs the IP address of the proxy server. You can go this route using the Nmap option `--proxies PROXY_URL`. For example, `nmap -sS -Pn --proxies PROXY_URL -F MACHINE_IP` will send all its packets via the proxy server you specify. Note that you can chain proxies using a comma-separated list.
