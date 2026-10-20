---
title: "Scannign a “Local” Network"
date: 2025-03-06 12:04:00 +0700
categories: ["TryHackMe", "Cyber 101", "Nmap"]
tags: ["tryhackme", "nmap"]
description: "Nmap offers the -sn option, i.e., ping scan. However, don’t expect this to be limited like ping. Let’s see this in action."
media_subpath: /assets/img/tryhackme/2025-03-06-scannign-a-local-network/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/nmap/scannign-a-local-network/
th_id: "cyber-101/nmap/scannign-a-local-network"
th_parent: "cyber-101/nmap"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/nmap"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/nmap"]
---

{% include tryhackme-nav.html %}

Nmap offers the `-sn` option, i.e., ping scan. However, don’t expect this to be limited like `ping`. Let’s see this in action.

![image.png](image.png)

Because we are scanning the local network, where we are connected via Ethernet or WiFi, we can look up the MAC addresses of the devices. Consequently, we can figure out the network card vendors, which is beneficial information as it can help us guess the type of target device(s).

When scanning a directly connected network, Nmap starts by sending ARP requests. When a device responds to the ARP request, Nmap labels it with “Host is up”.

As we mentioned earlier, `-sn` aims to discover live hosts without attempting to discover the services running on them. This scan might be helpful if you want to discover the devices on a network without causing much noise. However, this won’t tell us which services are running. If we want to learn more about the network services running on the live hosts, we need a more “noisy” type of scan, which we will explore in the next task.

As a final point, Nmap offers a list scan with the option `-sL`. This scan only lists the targets to scan without actually scanning them. For example, `nmap -sL 192.168.0.1/24` will list the 256 targets that will be scanned. This option helps confirm the targets before running the actual scan.
