---
title: "FAT32 Structure"
date: 2025-08-21 12:52:00 +0700
categories: ["TryHackMe", "SOC LV 2", "FAT32 Analysis"]
tags: ["tryhackme", "fat32-analysis"]
description: "A FAT32 partitioned volume typically consists of the following parts:"
media_subpath: /assets/img/tryhackme/2025-08-21-fat32-structure/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/fat32-analysis/fat32-structure/
th_id: "soc-lv-2/fat32-analysis/fat32-structure"
th_parent: "soc-lv-2/fat32-analysis"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/fat32-analysis"
th_size: 3
th_ancestors: ["soc-lv-2", "soc-lv-2/fat32-analysis"]
---

{% include tryhackme-nav.html %}

### **FAT32 Structure**

A FAT32 partitioned volume typically consists of the following parts:

- Reserved Area
    - Boot sector, also named VBR
    - FSinfo Sector (FS is an acronym for Filesystem)
    - Reserved Sectors
- FAT Area
    - File Allocation Table (FAT1)
    - Backup File Allocation Table (FAT2)
- Data Area
    - Root Directory
    - Data Region

## **1. Reserved Area**

contains the important filesystem structures required for the volume to function. The reserved sector always starts from sector 0 on the partition and includes:

- Boot sector
- FSinfo sector
- Backup boot sector
- Additional reserved sectors

| **Field** | **Sector number** |
| --- | --- |
| Boot sector | 0 |
| FSinfo sector | 1 |
| Backup boot sector | 6 |
| Additional reserved sectors | Starting from sector 7 until the start of the File Allocation Table |

How do we need to interpret this table? A sector is the smallest addressable unit on a disk. In most cases the size of a sector is 512 bytes. So, if we apply this info to the table above, it means the following:

- The boot sector starts at sector 0 and encompasses 512 bytes.
- The FSinfo sector starts at sector 1 and encompasses 512 bytes.
- Sectors 2 to 5 are reserved sectors. The total size is 4 times 512 bytes, which equals 2048 bytes.
- The backup boot sector starts at sector 6 and encompasses 512 bytes.
- The additional reserved sectors start from sector 7 and stretch until the start of the FAT area. We need to analyze the boot sector to determine the complete size of the Reserved Area.

### **1.1.**

[**Boot Sector**]({{ site.baseurl }}/tryhackme/soc-lv-2/fat32-analysis/fat32-structure/boot-sector/)

### 1.2.

[**FAT Area**]({{ site.baseurl }}/tryhackme/soc-lv-2/fat32-analysis/fat32-structure/fat-area/)

### 1.3

[**Data Area**]({{ site.baseurl }}/tryhackme/soc-lv-2/fat32-analysis/fat32-structure/data-area/)
