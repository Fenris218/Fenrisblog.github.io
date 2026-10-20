---
title: "Port scanning"
date: 2025-03-07 13:05:00 +0700
categories: ["TryHackMe", "Cyber 101", "Nmap"]
tags: ["tryhackme", "nmap"]
description: "Connect Scan"
media_subpath: /assets/img/tryhackme/2025-03-07-port-scanning/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/nmap/port-scanning/
th_id: "cyber-101/nmap/port-scanning"
th_parent: "cyber-101/nmap"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/nmap"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/nmap"]
---

{% include tryhackme-nav.html %}

- **Cách đơn giản nhất để biết một cổng TCP có “mở” hay không** là **thử kết nối TCP tới cổng đó** (ví dụ dùng `telnet host port`).
    - Khi bạn mở kết nối TCP, bạn cố hoàn tất **3-way handshake** (SYN → SYN/ACK → ACK).
    - **Chỉ những cổng đang mở** mới trả lời bằng **SYN/ACK** và cho phép kết nối hoàn tất — rồi bạn sẽ thấy “Connected” hoặc một prompt telnet.
    - Nếu cổng đóng, bạn sẽ nhận **RST** (connection refused). Nếu bị tường lửa lọc, bạn có thể **không nhận gì** (timeout).

**Connect Scan**

- **Nmap’s connect scan** (`sT`) làm đúng việc này: nó dùng hàm `connect()` của hệ điều hành để **thực sự mở một kết nối TCP** tới từng port — giống như bạn dùng telnet nhưng tự động và lặp cho nhiều port/host.

![image.png](image.png)

(In the screenshot below, our scanning machine has the IP address `192.168.124.148` and the target system has TCP port 22 open and port 23 closed. In the part marked with 1, you can see how the TCP three-way handshake was completed and later torn down with a TCP RST-ACK packet by Nmap. The part marked with 2 shows a connection attempt to a closed port, and the target system responded with a TCP RST-ACK packet.)

### **SYN Scan (Stealth)**

Không giống như connect scan phải hoàn tất TCP handshake thì **SYN scan** (hay *half-open* / *stealth scan*) chỉ gửi **gói TCP SYN** — bước 1 của 3-way handshake. Nó **không hoàn tất** handshake. Dựa vào phản hồi (SYN/ACK, RST, hoặc không trả lời) ta suy ra trạng thái cổng. Ở `nmap` dùng `-sS`.

![image.png](image%201.png)

### **Scanning UDP Ports**

Although most services use TCP for communication, many use UDP. Examples include DNS, DHCP, NTP (Network Time Protocol), SNMP (Simple Network Management Protocol), and VoIP (Voice over IP). UDP does not require establishing a connection and tearing it down afterwards. Furthermore, it is very suitable for real-time communication, such as live broadcasts. All these are reasons to consider scanning for and discovering services listening on UDP ports.

Nmap offers the option `-sU` to scan for UDP services. Because UDP is simpler than TCP, we expect the traffic to differ.

### **Limiting the Target Ports**

Nmap scans the most common 1,000 ports by default. However, this might not be what you are looking for. Therefore, Nmap offers you a few more options.

- `F` is for Fast mode, which scans the 100 most common ports (instead of the default 1000).
- `p[range]` allows you to specify a range of ports to scan. For example, `p10-1024` scans from port 10 to port 1024, while `p-25` will scan all the ports between 1 and 25. Note that `p-` scans all the ports and is equivalent to `p1-65535` and is the best option if you want to be as thorough as possible.

## NULL, FIN and Xmas TCP port scans

 are less commonly used than any of the others we've covered already. All three are interlinked and are used primarily as they tend to be even stealthier, relatively speaking, than a SYN "stealth" scan.

- As the name suggests, NULL scans (`-sN`) are when the TCP request is sent with no flags set at all. As per the RFC, the target host should respond with a RST if the port is closed.

![image.png](image%202.png)

- FIN scans (`-sF`) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed.

![image.png](image%203.png)

- As with the other two scans in this class, Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN)
