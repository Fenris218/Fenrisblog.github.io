---
title: "Boot process"
date: 2025-08-17 08:48:00 +0700
categories: ["TryHackMe", "SOC LV 2", "MBR and GPT"]
tags: ["tryhackme", "mbr-and-gpt"]
description: "BIOS (Basic Input/Output System) and UEFI (Unified Extensible Firmware Interface) are responsible for verifying whether all the hardware components work prop…"
media_subpath: /assets/img/tryhackme/2025-08-17-boot-process/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/mbr-and-gpt/boot-process/
th_id: "soc-lv-2/mbr-and-gpt/boot-process"
th_parent: "soc-lv-2/mbr-and-gpt"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/mbr-and-gpt"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/mbr-and-gpt"]
---

{% include tryhackme-nav.html %}

**BIOS** (Basic Input/Output System) and **UEFI** (Unified Extensible Firmware Interface) are responsible for verifying whether all the hardware components work properly. 

- **BIOS** has been used for decades and is still used in some hardware. It runs in the basic 16-bit mode and supports only up to 2 terabytes of disks. The most important thing to note is that  supports the MBR partitioning scheme,
- **UEFI** came as a replacement for BIOS, offering 32-bit and 64-bit modes with up to 9 zettabytes of disks.  offers a secure boot feature to ensure  during the system boot process. It also offers redundancy, allowing us to recover from the backup even if the boot code is corrupted.  uses a GPT partitioning scheme, unlike the MBR partitioning scheme used by BIOS

![image.png](image.png)

## **Power-On-Self-Test (POST)**

The system is now powered on, and the CPU has executed instructions from the firmware (BIOS/UEFI) installed. The BIOS/UEFI then starts a Power-On-Self-Test to ensure all the system’s hardware components are working fine. 

![image.png](image%201.png)

## **Locate the Bootable Device**

After the BIOS/UEFI has performed the POST check, it is time for the BIOS/UEFI to locate bootable devices, such as SSDs, HDDs, or USBs, with the operating system installed. Once the bootable device is located, it starts reading this device. Now, here comes the role of the **MBR/GPT**. The very first sector of the device would either contain the MBR (Master Boot Record) or the GPT (GUID Partition Table). The MBR/GPT would be taking control of the boot process from here.
