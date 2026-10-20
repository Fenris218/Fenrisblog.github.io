---
title: "Analysis Techniques and Tools"
date: 2025-08-25 16:56:00 +0700
categories: ["TryHackMe", "SOC LV 2", "FAT32 Analysis"]
tags: ["tryhackme", "fat32-analysis"]
description: "Data Recovery and Content Analysis"
media_subpath: /assets/img/tryhackme/2025-08-25-analysis-techniques-and-tools/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/fat32-analysis/analysis-techniques-and-tools/
th_id: "soc-lv-2/fat32-analysis/analysis-techniques-and-tools"
th_parent: "soc-lv-2/fat32-analysis"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/fat32-analysis"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/fat32-analysis"]
---

{% include tryhackme-nav.html %}

## **1. Filesystem Analysis Techniques**

| **Analysis Technique** | **Related FAT32 Field(s)** | **Description** |
| --- | --- | --- |
| Cluster Chain Analysis | File Allocation Table (FAT), Root Directory Entries | Tracks and analyzes cluster chains to reconstruct fragmented files and detect allocation anomalies. |
| Directory Structure and File Name Analysis | Directory Entries (`File Name`, `Attributes`, `First Cluster`) | Investigates file names, attributes, and directory structures for hidden or deleted files. |
| Volume Serial Number and Boot Sector Analysis | Boot Sector (`BPB`), Volume Metadata | Analyzes metadata such as volume label, serial number, sector size, and file system version for tampering or inconsistencies. |
| Analyzing FAT Table Corruption or Manipulation | FAT, Backup FAT, Root Directory | Detects inconsistencies or tampering by comparing the primary FAT with its backup and analyzing cluster allocation. |
| Examining System Volume Information (Windows only) | Reserved Metadata Files, Root Directory | Analyzes Windows-specific system files, such as `System Volume Information`, for user activity or tampering evidence. |
| Corruption and Tampering Detection | FAT, Boot Sector, Directory Entries | Detects tampering or corruption by verifying file system structures and metadata integrity. |

**Data Recovery and Content Analysis**

This category focuses on recovering deleted or hidden data, checking data in allocated and unallocated spaces

| **Analysis Technique** | **Related FAT32 Field(s)** | **Description** |
| --- | --- | --- |
| File Carving | Unallocated Clusters, Data Area | Recovers files by searching for file headers/footers or specific patterns in unallocated space. |
| Slack Space Analysis | Data Clusters, Directory Entries | Examines unused space within allocated clusters for residual or hidden data. |
| Deleted File Recovery | Directory Entries (`Status Byte`, `First Cluster`), FAT | Recovers deleted files by analyzing directory entries marked as deleted and reconstructing cluster chains. |
| Keyword and Pattern Search | Unallocated Clusters, Data Area | Searches for specific strings, patterns, or file signatures across allocated and unallocated space for evidence. |
| Timeline Analysis | `Last Access Date`, `Creation Date/Time`, `Last Modified Date/Time` | Builds a timeline of file and folder activities using timestamps from directory entries. |
|  |  |  |
