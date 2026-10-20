---
title: "Detecting PSEXEC lateral movement"
date: 2025-10-04 08:36:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Active Directory"]
tags: ["tryhackme", "active-directory"]
description: "When an attacker already has an authenticated SMB session (via net use) and runs PsExec.exe \\\\target cmd.exe, the following happens:"
media_subpath: /assets/img/tryhackme/2025-10-04-detecting-psexec-lateral-movement/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/active-directory/detecting-ad-lateral-movement/detecting-psexec-lateral-movement/
th_id: "soc-lv-2/active-directory/detecting-ad-lateral-movement/detecting-psexec-lateral-movement"
th_parent: "soc-lv-2/active-directory/detecting-ad-lateral-movement"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/active-directory"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/active-directory", "soc-lv-2/active-directory/detecting-ad-lateral-movement"]
---

{% include tryhackme-nav.html %}

## **How PsExec Works**

When an attacker already has an authenticated SMB session (via `net use`) and runs `PsExec.exe \\target cmd.exe`, the following happens:

1. PsExec connects to the target's `ADMIN$` share over SMB
2. It copies a service binary (`PSEXESVC.exe`) to the target's `C:\Windows` directory
3. It creates and starts a new Windows service on the target (System Event 7045)
4. The service creates named pipes for `stdin`/`stdout`/`stderr` communication (Sysmon Event 17)
5. That service executes whatever command the attacker specified
6. When the session ends, PsExec removes the service and cleans up the binary

Event 7045 (A New Service Was Installed) in the System log is the signature artifact for PsExec, logged on the **destination** machine. This is what distinguishes PsExec from plain SMB access.
