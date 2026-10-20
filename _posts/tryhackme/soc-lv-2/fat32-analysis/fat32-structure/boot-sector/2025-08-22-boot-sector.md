---
title: "Boot Sector"
date: 2025-08-22 13:53:00 +0700
categories: ["TryHackMe", "SOC LV 2", "FAT32 Analysis"]
tags: ["tryhackme", "fat32-analysis"]
description: "It contains the metadata of the partition. This information is essential for the OS to know how to access the partition, where to look for the File Allocatio…"
media_subpath: /assets/img/tryhackme/2025-08-22-boot-sector/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/fat32-analysis/fat32-structure/boot-sector/
th_id: "soc-lv-2/fat32-analysis/fat32-structure/boot-sector"
th_parent: "soc-lv-2/fat32-analysis/fat32-structure"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/fat32-analysis"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/fat32-analysis", "soc-lv-2/fat32-analysis/fat32-structure"]
---

{% include tryhackme-nav.html %}

It contains the metadata of the partition. This information is essential for the OS to know how to access the partition, where to look for the File Allocation Table, where the Root Directory is located, and where the Data Region begins. 

| **Field** | **Subfield** | **Size (bytes)** | **Offset (Hex)** | **Explanation** |
| --- | --- | --- | --- | --- |
| Jump Instruction |  | 3 |  | Allows the BIOS or bootloader to bypass the BIOS Parameter Block (BPB) and start executing the boot code. |
| OEM Name |  | 8 |  | Contains the name of the Original Equipment Manufacturer that formatted the disk (Can refer to physical or logical disk). |
| BIOS Parameter Block (BPB) |  |  |  | Contains essential metadata about the volume. Without this, the OS could not read the partitioned volume. |
|  | Bytes per Sector | 2 |  | Lists the size of a sector. The standard sector size is often 512 bytes. |
|  | Sectors per Cluster | 1 |  | How many sectors are used to form a cluster? A cluster is the smallest addressable unit to store a file. |
|  | Reserved Sectors | 2 |  | How many sectors are reserved for metadata storage? |
|  | Number of FATs | 1 |  | How many File Allocation Table instances are on the partition. The standard value for this is 2. The FAT table and its backup (Named FAT1 and FAT2) |
|  | Maximum Root Directory Entries | 2 |  | How many entries can the root directory contain. For FAT32, this is set to 0 because the root directory can dynamically grow. |
|  | Total Sectors | 2 or 4 |  | The total number of sectors on the formatted volume. This field is 0 for FAT32. |
|  | Media Descriptor | 1 |  | Describes what type of media the partition is present on. For example, 0xF8 means that the media is a fixed hard disk. Note: Modern OSs don’t set this value accurately anymore. They generally use the value 0xF8 for a fixed disk or a USB drive. |
|  | Sectors per FAT | 2 |  | Lists how large the File Allocation Table is. |
|  | Sectors per Track | 2 |  | This field refers to the parts of a mechanical hard drive. |
|  | Number of Heads | 2 |  | This field refers to the parts of a mechanical hard drive. |
|  | Hidden sectors | 4 |  | Used to indicate the number of sectors before the start of the current partition when the partition does not start at the physical beginning of the disk. |
|  | Total Sectors 32 | 4 |  | The total amount of sectors on the partition expressed in 32-bit. This field can't be zero for FAT32 volumes |
| Extended BPB |  |  |  | Extends the BPB with additional data specific to the FAT32 filesystem. |
|  | Sectors per FAT | 4 |  | The number of sectors assigned to the File Allocation Table. If there is a backup FAT, it will also take the same size. |
|  | Flags | 2 |  | This value refers to the mirroring of the FAT table. In other words, is there a backup configured? If the value is 0, mirroring is enabled. |
|  | Version |  |  | Refers to the version of the FAT32 filesystem. Typically this is V0.0. |
|  | Cluster Root Directory | 4 |  | Points to the cluster number that the root directory is located at relative to the beginning of the data area. |
|  | FSInfo Sector | 2 |  | Contains information about the free clusters and the next available cluster. |
|  | Backup Boot Sector | 2 |  | Points at the cluster that has a copy of the boot sector. |
| Boot Code |  | 420 |  | Contains the data the BIOS needs to boot up. |
| Boot Sector Signature |  | 2 |  | Used for validation of the boot sector. |

Ví dụ 

![image.png](image.png)

| **Field** | **Offset** | **Address** | **Hex Value (Little Endianess)** | **Hex Value To Translate** | **Translated Value** | **Explanation** |
| --- | --- | --- | --- | --- | --- | --- |
| Jump instruction | 0000 0000 | 00 | EB | EB | jmp short $0000005A | Jump to address. |
|  |  | 01 | 58 | 58 | Represents 88 bytes in hex. | This is the number of bytes to jump over. |
|  |  | 02 | 90 | 90 | NOP | This instruction does nothing. It is added for padding. |
| OEM name | 0000 0000 | 03-0A | 4D 53 44 4F 53 35 2E 30 | - | MSDOS5.0 | This value indicates that the partition was formatted with a tool using MS-DOS version 5.0 |
| Bytes per Sector | 0000 0000 | 0B-0C | 00 02 | 02 00 | 512 | 1 sector has a size of 512 bytes |
| Sectors per Cluster | 0000 0000 | 0D | 01 | 01 | 1 | 1 cluster has 1 sector. This is often not the case. Clusters of 4KB are used most of the time. |
| Reserved Sectors | 0000 0000 | 0E-0F | 7E 18 | 18 7E | 6270 | The amount of reserved sectors, including the boot sector, is 6270. After that, the FAT1 starts. |
| Number of FATs | 0000 0010 | 00 | 02 | 02 | 2 | The partition has 1 FAT table and a backup. Respectively named FAT1 and FAT2. |
| Maximum Root DirectoryEntries | 0000 0010 | 01-02 | 00 00 | 00 00 | 0 | This is not used in FAT32. |
| Total Sectors | 0000 0010 | 03-04 | 00 00 | 00 00 | 0 | NA for FAT32. The Total Sectors 32 value of the extended BPB will be used. |
| Media Descriptor | 0000 0010 | 05 | F8 | F8 |  | Fixed disk |
| Sectors per FAT | 0000 0010 | 06-07 | 00 00 | 00 00 | 0 | This field is used for FAT16 and not for FAT32. This can be discarded |
| Sectors per Track | 0000 0010 | 08-09 | 3F 00 | 00 3F | 63 | A track on a hard drive platter contains 255 sectors. This is a logical placeholder used for compatibility. It does not represent real physical disk tracks. |
| Number of Heads | 0000 0010 | 0A-0B | FF 00 | 00 FF | 255 | The total heads of the hard drive is 255. This value is a logical placeholder used for compatibility. It does not represent real physical disk heads. |
| Hidden sectors | 0000 0010 | 0C-0F | 00 F8 30 06 | 06 30 F8 00 | 103872512 | If we multiply this value with the sector size and then convert it to GB, it comes down to 49GB, which is the size of the `C:\` partition. |
| Total sectors 32 | 0000 0020 | 00-03 | 00 00 02 00 | 00 02 00 00 | 131072 | If we multiply this value with the sector size and then convert it to MB, it comes down to 64MB, which is the size of the image. |
| Sectors per FAT | 0000 0020 | 04-07 | C1 03 00 00 | 00 00 03 C1 | 961 | amount of sectors assigned to the FAT1 and FAT2 (2 times 961). |
| Flags | 0000 0020 | 08-09 | 00 00 | 00 00 | 00 | This means FAT mirroring is enabled. FAT entries are simultaneously written to FAT1 and FAT2 |
| Version | 0000 0020 | 0A-0B | 00 00 | 00 00 | 0 | FAT32 version is 0.0 |
| Cluster Root Directory | 0000 0020 | 0C-0D | 02 00 | 00 02 |  | The root directory is located at the 2nd cluster of the data region. |
| FS Info Sector | 0000 0030 | 00-02 | 01 00 | 00 01 | 1 | information about the free clusters and the next available cluster is located at sector 1 (right behind the boot sector) |
| Backup Boot Sector | 0000 0030 | 02-03 | 06 00 | 00 06 | 6 | Sector 6 contains the backup for our boot information. |
| Boot Code | 00000030-000001F0 | 0E-0D | - | - | - | Contains the boot code necessary for the BIOS or UEFI to boot up the volume. |
| Boot Sector Signature | 0000 01F0 | 0E-0F | 55 AA | - | - | Indicates that the current sector is bootable |
