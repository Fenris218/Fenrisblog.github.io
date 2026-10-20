---
title: "Window API"
date: 2025-08-05 08:36:00 +0700
categories: ["TryHackMe", "SOC LV1", "Window API"]
tags: ["tryhackme", "window-api"]
description: "WIN API, is a library to interface between user-mode applications and the kernel"
media_subpath: /assets/img/tryhackme/2025-08-05-window-api/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/window-api/
th_id: "soc-lv1/window-api"
th_parent: "soc-lv1"
th_kind: module
th_order: 22
th_course: "soc-lv1"
th_module: "soc-lv1/window-api"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

WIN API, is a library to interface between user-mode applications and the kernel

Windows distinguishes hardware access by two distinct modes: **user** and **kernel mode**. These modes determine the hardware, kernel, and memory access an application or driver is permitted. API or system calls interface between each mode, sending information to the system to be processed in kernel mode.

![image.png](image.png)

https://learn.microsoft.com/en-us/windows/win32/apiindex/windows-api-list

## 2. Commonly Abused API Calls

| **API Call** | **Explanation** |
| --- | --- |
| LoadLibraryA | Maps a specified DLL  into the address space of the calling process |
| GetUserNameA | Retrieves the name of the user associated with the current thread |
| GetComputerNameA | Retrieves a NetBIOS or DNS  name of the local computer |
| GetVersionExA | Obtains information about the version of the operating system currently running |
| GetModuleFileNameA | Retrieves the fully qualified path for the file of the specified module and process |
| GetStartupInfoA | Retrieves contents of STARTUPINFO structure (window station, desktop, standard handles, and appearance of a process) |
| GetModuleHandle | Returns a module handle for the specified module if mapped into the calling process's address space |
| GetProcAddress | Returns the address of a specified exported DLL  function |
| VirtualProtect | Changes the protection on a region of memory in the virtual address space of the calling process |
