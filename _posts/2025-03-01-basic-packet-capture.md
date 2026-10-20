---
title: "Basic Packet Capture"
date: 2025-03-01 19:59:00 +0700
categories: ["TryHackMe", "Cyber 101", "TCPdump : ghi gói tin thông qua CLI"]
tags: ["tryhackme", "tcpdump-ghi-goi-tin-thong-qua-cli"]
description: "The first thing to decide is which network interface to listen to using -i INTERFACE. You can choose to listen on all available interfaces using -i any; alte…"
media_subpath: /assets/img/tryhackme/2025-03-01-basic-packet-capture/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli/basic-packet-capture/
th_id: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli/basic-packet-capture"
th_parent: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/tcpdump-ghi-goi-tin-thong-qua-cli"]
---

{% include tryhackme-nav.html %}

### Specify the Network Interface

The first thing to decide is which network interface to listen to using `-i INTERFACE`. You can choose to listen on all available interfaces using `-i any`; alternatively, you can specify an interface you want to listen on, such as `-i eth0`

A command such as `ip address show` (or merely `ip a s`) would list the available network interfaces. 

```bash
user@ip-10-48-170-132:~$ ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 02:69:f1:76:41:3f brd ff:ff:ff:ff:ff:ff
    altname enp0s5
    inet 10.48.170.132/18 brd 10.48.191.255 scope global dynamic ens5
       valid_lft 3237sec preferred_lft 3237sec
    inet6 fe80::69:f1ff:fe76:413f/64 scope link 
       valid_lft forever preferred_lft forever
user@ip-10-48-170-132:~$ 

```

### Save the Captured Packets

In many cases, you should check the captured packets again later. This can be achieved by saving to a file using `-w FILE`. The file extension is most commonly set to `.pcap`

### Read Captured Packets from a File

You can use Tcpdump to read packets from a file by using `-r FILE`

### Limit the Number of Captured Packets

You can specify the number of packets to capture by specifying the count using `-c COUNT`

### Don’t Resolve IP Addresses and Port Numbers

Tcpdump will resolve IP addresses and print friendly domain names where possible. To avoid making such DNS lookups, you can use the `-n` argument. Similarly, if you don’t want port numbers to be resolved, such as `80` being resolved to `http`, you can use the `-nn` to stop both DNS and port number lookups.

### Produce (More) Verbose Output

If you want to print more details about the packets, you can use `-v` to produce a slightly more verbose output. According to the Tcpdump manual page (`man tcpdump`), the addition of `-v` will print “the time to live, identification, total length and options in an IP packet” among other checks. The `-vv` will produce more verbose output; the `-vvv` will provide even more verbosity; check the manual page for details.

Example

```bash
tcpdump -i ens5 -c 5 -n
```
