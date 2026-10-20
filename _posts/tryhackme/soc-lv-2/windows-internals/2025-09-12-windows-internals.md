---
title: "Windows Internals"
date: 2025-09-12 10:14:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Windows Internals"]
tags: ["tryhackme", "windows-internals"]
description: "A process has many components, The Microsoft docs(opens in new tab) break down these other components, \"Each process provides the resources needed to execute…"
media_subpath: /assets/img/tryhackme/2025-09-12-windows-internals/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/windows-internals/
th_id: "soc-lv-2/windows-internals"
th_parent: "soc-lv-2"
th_kind: module
th_order: 6
th_course: "soc-lv-2"
th_module: "soc-lv-2/windows-internals"
th_size: 0
th_ancestors: ["soc-lv-2"]
---

{% include tryhackme-nav.html %}

## 1. Process

 A process has many components, The [Microsoft docs(opens in new tab)](https://docs.microsoft.com/en-us/windows/win32/procthread/about-processes-and-threads) break down these other components, "Each process provides the resources needed to execute a program. A process has a virtual address space, executable code, open handles to system objects, a security context, a unique process identifier, environment variables, a priority class, minimum and maximum working set sizes, and at least one thread of execution

| **Process Component** | **Purpose** |
| --- | --- |
| Private Virtual Address Space | Virtual memory addresses that the process is allocated. |
| Executable Program | Defines code and data stored in the virtual address space. |
| Open Handles | Defines handles to system resources accessible to the process. |
| Security Context | The access token defines the user, security groups, privileges, and other security information. |
| Process ID | Unique numerical identifier of the process. |
| Threads | Section of a process scheduled for execution. |

We can also explain a process at a lower level as it resides in the virtual address space.

| **Component** | **Purpose** |
| --- | --- |
| Code | Code to be executed by the process. |
| Global Variables | Stored variables. |
| Process Heap | Defines the heap where data is stored. |
| Process Resources | Defines further resources of the process. |
| Environment Block | Data structure to define process information. |

## 2. Thread

Threads share the same details and resources as their parent process, such as code, global variables, etc. Threads also have their unique values and data, outlined in the table below.

| **Component** | **Purpose** |
| --- | --- |
| Stack | All data relevant and specific to the thread (exceptions, procedure calls, etc.) |
| Thread Local Storage | Pointers for allocating storage to a unique data environment |
| Stack Argument | Unique value assigned to each thread |
| Context Structure | Holds machine register values maintained by the kernel |

## 3. Virtual Memory

Virtual memory allows other internal components to interact with memory as if it was physical memory without the risk of collisions between applications.

Virtual memory provides each process with a [private virtual address space(opens in new tab)](https://docs.microsoft.com/en-us/windows/win32/memory/virtual-address-space). A memory manager is used to translate virtual addresses to physical addresses. By having a private virtual address space and not directly writing to physical memory, processes have less risk of causing damage.
