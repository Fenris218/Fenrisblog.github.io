---
title: "x86 Architecture"
date: 2025-08-12 15:43:00 +0700
categories: ["TryHackMe", "SOC LV 2", "x86 Architecture"]
tags: ["tryhackme", "x86-architecture"]
description: "General-Purpose Registers"
media_subpath: /assets/img/tryhackme/2025-08-12-x86-architecture/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/x86-architecture/
th_id: "soc-lv-2/x86-architecture"
th_parent: "soc-lv-2"
th_kind: module
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/x86-architecture"
th_size: 0
th_ancestors: ["soc-lv-2"]
---

{% include tryhackme-nav.html %}

## 1. Registers

**General-Purpose Registers**

- EAX-RAX : Accumulator Register. Results of arithmetic operations are often stored in this register.
- EBX-RBX :  Base Register, which is often used to store the Base address for referencing an offset.
- ECX-RCX : This register is also called the Counter Register and is often used in counting operations such as loops
- EDX-RDX : This register is also called the Data Register. It is often used in multiplication/division operations
- ESP-RSP : Stack pointer. It points to the top of the stack
- EBP-RBP : Base Pointer. It is used to access parameters passed by the stack.
- ESI-RSI : Source Index register. It is used for string operations. It is used with the Data Segment (DS) register
- EDI-RDI : Destination Index register. It is also used for string operations. It is used with the Extra Segment (ES) register
- R8-R15 :

![image.png](image.png)

**Segment Registers:**

Segment Registers are 16-bit registers that convert the flat memory space into different segments for easier addressing. 

- **Code Segment:** The Code Segment (CS ) register points to the Code section in the memory.
- **Data Segment:** The Data Segment (DS) register points to the program's data section in the memory.
- **Stack Segment:** The Stack Segment (SS) register points to the program's Stack in the memory.
- **Extra Segments (ES, FS, and GS):** These extra segment registers point to different data sections. These and the DS register divide the program's memory into four distinct data sections.

## 2. Memory

- Code : contains the program's code.
- Data : The Data section contains initialized data that is not variable and remains constant.
- Heap : The heap, also known as dynamic Memory, contains variables and data created and destroyed during program execution.
- Stack : This section of the Memory contains local variables, arguments passed on to the program, and the return address of the parent process that called the program. Since the return address is related to the control flow of the CPU's instructions, the stack is often targeted by malware to hijack the control flow

![image.png](4599b46b-0ab5-4498-81b0-997ffb01c326.png)

## 3. Stack

![image.png](image%201.png)
