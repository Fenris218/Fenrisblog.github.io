---
title: "T1564.001 Hidden Files and Directories"
date: 2025-08-26 17:57:00 +0700
categories: ["TryHackMe", "SOC LV 2", "FAT32 Analysis"]
tags: ["tryhackme", "fat32-analysis"]
description: "To find hidden files or directories on a FAT32 image, we will need to analyze the SFN entries in the Root Directory. We can apply the analysis technique of D…"
media_subpath: /assets/img/tryhackme/2025-08-26-t1564-001-hidden-files-and-directories/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/fat32-analysis/t1564-001-hidden-files-and-directories/
th_id: "soc-lv-2/fat32-analysis/t1564-001-hidden-files-and-directories"
th_parent: "soc-lv-2/fat32-analysis"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/fat32-analysis"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/fat32-analysis"]
---

{% include tryhackme-nav.html %}

## **Manual Analysis**

To find hidden files or directories on a FAT32 image, we will need to analyze the SFN entries in the Root Directory. We can apply the analysis technique of **Directory Structure and File Name Analysis** from Data Area

Remember that an SFN entry is 32 bytes long. We are interested in the value of the 12th byte of the SFN entry. This byte represents the attributes of a file or directory. The file or directory is hidden if the byte is set to `0x02`.

Example : Let’s look at the FAT32 image that the user found. In the image below, we can see that there are multiple entries, Once the image has loaded, press `CTRL+G` and enter the hex value  400000 (This value is determined by analyzing the boot sector) to navigate to the `root directory` 

![image.png](image.png)

Let’s look at each of them and see which entries are hidden. But before that, we should first check if the `root directory` is not **fragmented** (split over multiple clusters); otherwise, we could miss valuable information. In our case, the directory entries and file entries are split. For efficiency reasons, Windows often splits the file and directory entries and maps them to a different cluster. There are `root directory entries` on the clusters starting with offsets `00400200` and `00400600`.

**Directories**

![image.png](image%201.png)

The first entry is an LFN entry that links to the second one, an SFN entry. Let’s zoom in on the SFN entry starting at offset `004000A0`.

| **Offset** | **Size** | **Field Name** | **Value (Hex)** | **Meaning** |
| --- | --- | --- | --- | --- |
| `0x00` | 8 bytes | File Name | `4D 40 4C 4C 30 56 33 20` | “M@LL0V3” |
| `0x08` | 3 bytes | File Extension | `20 20 20` | Space-filled (no file extension) |
| `0x0B` | 1 byte | File Attributes | `13` | Read-only + Hidden + Directory (0x01 + 0x02 + 0x10) |
| `0x0C` | 1 byte | Reserved (NT) | `00` | Reserved for NT (unused, zero-filled) |
| `0x0D` | 1 byte | Creation Time (tenths) | `B6` | 182 tenths of a second |
| `0x0E` | 2 bytes | Creation Time | `CD 81` | Time: 16:14:26 (binary decoded as hours:minutes:seconds) |
| `0x10` | 2 bytes | Creation Date | `94 59` | Date: **Friday, December 20th, 2024** (binary decoded as year, month, day) |
| `0x12` | 2 bytes | Last Access Date | `94 59` | Date: **Friday, December 20th, 2024** (same as creation date) |
| `0x14` | 2 bytes | High-Order Cluster Number | `00 00` | High word of the first cluster |
| `0x16` | 2 bytes | Last Modification Time | `CE 81` | Time: ‏‎16:14:28 |
| `0x18` | 2 bytes | Last Modification Date | `94 59` | Date: **Friday, December 20th, 2024** |
| `0x1A` | 2 bytes | First Cluster Number | `05 00` | Cluster 5 |
| `0x1C` | 4 bytes | File Size | `00 00 00 00` | File size = 0 bytes => This indicates that the entry is a **directory** |

Based on the information in the table above, we can conclude the following things for this SFN entry:

- The entry represents a directory with the name `M@LL0v3`.
- The directory has the attributes `hidden` and `read-only`.
- It was created on December 20th, 2024 at 16:14:27.
- The directory contents start at cluster 5 (the actual cluster number is 3. The first two clusters should not be counted as they are virtual, reserved clusters).

**Files**

Navigate to the cluster starting with offset `00400200` by pressing `CTRL+G` in the HxD editor and entering the offset value. You should see the same entries displayed in the image below.

![image.png](image%202.png)

These entries are standard on a Windows FAT32 partition. Windows and its services use the `WPSettings.dat` file to store information related to indexing, backup, and more. The other entries refer to the `current directory (.)` and the `parent directory (..)`
