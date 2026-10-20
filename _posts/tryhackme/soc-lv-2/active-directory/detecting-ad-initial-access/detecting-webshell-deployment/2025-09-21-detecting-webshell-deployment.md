---
title: "Detecting Webshell deployment"
date: 2025-09-21 19:23:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "A web shell is a malicious script (usually with an .aspx extension in IIS environments) that lets an attacker execute OS commands through HTTP requests."
media_subpath: /assets/img/tryhackme/2025-09-21-detecting-webshell-deployment/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-initial-access/detecting-webshell-deployment/
th_id: "soc-lv-2/active-directory/detecting-ad-initial-access/detecting-webshell-deployment"
th_parent: "soc-lv-2/active-directory/detecting-ad-initial-access"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-initial-access"]
---

{% include tryhackme-nav.html %}

A web shell is a malicious script (usually with an `.aspx` extension in IIS environments) that lets an attacker execute OS commands through HTTP requests.

A basic web shell can be as simple as a single line:

```
<%@ Page Language="C#" %><%System.Diagnostics.Process.Start("cmd.exe","/c "+Request["cmd"]);%>

```

![image.png](image.png)

**The Core Detection Pattern**

Web shell activity has a distinct signature in process chains. During normal IIS operation, the worker process `w3wp.exe` handles HTTP requests and generates responses without launching other processes.

Meanwhile, when an attacker interacts with a web shell, `w3wp.exe` spawns child processes to execute commands: When `w3wp.exe` is spawning `cmd.exe`, `powershell.exe`, or tools that it shouldn't spawn, that's almost always worth investigating. Legitimate IIS applications rarely need to launch command shells.
