---
title: "Nmap Scans"
date: 2025-02-19 09:49:00 +0700
categories: ["TryHackMe", "Cyber 101", "Wireshark"]
tags: ["tryhackme", "wireshark"]
description: "tcp.flags.syn1 and tcp.flags.ack0 and tcp.window_size > 1024"
media_subpath: /assets/img/tryhackme/2025-02-19-nmap-scans/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/wireshark/traffic-analysis/nmap-scans/
th_id: "cyber-101/wireshark/traffic-analysis/nmap-scans"
th_parent: "cyber-101/wireshark/traffic-analysis"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/wireshark"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/wireshark", "cyber-101/wireshark/traffic-analysis"]
---

{% include tryhackme-nav.html %}

### TCP Scans

- TCP connected scans
- SYN scans
- UDP scans

| • Only SYN flag.<br>• SYN flag is set. The rest of the bits are not important. | • `tcp.flags == 2`<br>• `tcp.flags.syn == 1` |
| --- | --- |
| • Only ACK flag.<br>• ACK flag is set. The rest of the bits are not important. | • `tcp.flags == 16`<br>• `tcp.flags.ack == 1` |
| • Only SYN, ACK flags.<br>• SYN and ACK are set. The rest of the bits are not important. | • `tcp.flags == 18`<br>• `(tcp.flags.syn == 1) and (tcp.flags.ack == 1)` |
| • Only RST flag.<br>• RST flag is set. The rest of the bits are not important. | • `tcp.flags == 4`<br>• `tcp.flags.reset == 1` |
| • Only RST, ACK flags.<br>• RST and ACK are set. The rest of the bits are not important. | • `tcp.flags == 20`<br>• `(tcp.flags.reset == 1) and (tcp.flags.ack == 1)` |
| • Only FIN flag<br>• FIN flag is set. The rest of the bits are not important. | • `tcp.flags == 1`<br>• `tcp.flags.fin == 1` |

## TCP Connect Scans

- Relies on the three-way handshake (needs to finish the handshake process).
- Usually conducted with `nmap -sT` command.
- Used by **non-privileged users** (only option for a non-root user).
- Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol.
- The given filter shows the TCP Connect scan patterns in a capture file.

`tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024`

![image.png](image.png)

## SYN Scans

- Doesn't rely on the three-way handshake (no need to finish the handshake process).
- Usually conducted with `nmap -sS` command.
- Used by **privileged users**.
- Usually have a size less than or equal to 1024 bytes as the request is not finished and it doesn't expect to receive data.
- The given filter shows the TCP SYN scan patterns in a capture file.

`tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024`

![image.png](image%201.png)

## UDP Scans

- Doesn't require a handshake process
- No prompt for open ports
- ICMP error message for close ports
- Usually conducted with `nmap -sU` command.

![image.png](image%202.png)

![image.png](image%203.png)

the closed port returns an ICMP error packet

- The given filter shows the UDP scan patterns in a capture file.

`icmp.type==3 and icmp.code==3`
