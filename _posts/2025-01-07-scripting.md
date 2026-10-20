---
title: "Scripting"
date: 2025-01-07 14:06:00 +0700
categories: ["TryHackMe", "Cyber 101", "Window Fundamental"]
tags: ["tryhackme", "window-fundamental"]
description: "Invoke-Command -ComputerName Server01 -Credential Domain01\\User01 -ScriptBlock { Get-Culture } `"
media_subpath: /assets/img/tryhackme/2025-01-07-scripting/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/window-fundamental/powershell/scripting/
th_id: "cyber-101/window-fundamental/powershell/scripting"
th_parent: "cyber-101/window-fundamental/powershell"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/window-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/window-fundamental", "cyber-101/window-fundamental/powershell"]
---

{% include tryhackme-nav.html %}

- the `Invoke-Command` cmdlet:  is essential for executing commands on remote systems

```bash
Invoke-Command -FilePath C:\scripts\test.ps1 -ComputerName Server01

Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock {
        Get-Culture
    }
```
