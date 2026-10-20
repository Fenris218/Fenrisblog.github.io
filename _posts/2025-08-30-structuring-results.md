---
title: "Structuring Results"
date: 2025-08-30 09:01:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: "Imagine you are reviewing Sysmon process creation events and want to understand their logon context: did a process originate from a remote session (LogonType…"
media_subpath: /assets/img/tryhackme/2025-08-30-structuring-results/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/splunk-exploring-spl/structuring-results/
th_id: "soc-lv-2/advanced-splunk/splunk-exploring-spl/structuring-results"
th_parent: "soc-lv-2/advanced-splunk/splunk-exploring-spl"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/splunk-exploring-spl"]
---

{% include tryhackme-nav.html %}

- table

| **Command** | **Example** | **Explanation** |
| --- | --- | --- |
| `head` | `index=windowslogs | head 20` | Returns the first (newest) 20 events. Useful to speed up the search if you don't need complete results |
| `tail` | `index=windowslogs | tail 20` | Returns the last (oldest) 10 events. Useful to speed up the search if you don't need complete results |
| `sort` | `index=windowslogs | sort User` | This will sort the logs in alphabetical order based on the field `User` |
| `reverse` | `index=windowslogs | reverse` | This command reverses the order of events (descending order) |
- subsearches :

Imagine you are reviewing Sysmon process creation events and want to understand their logon context: did a process originate from a remote session (**LogonType 3/10**) or a service (**LogonType 5**)? Sysmon doesn't log the **LogonType** field, so you need to correlate across two data sources: Sysmon ID **1** for the process creation, and Security ID **4624** for the logon context. The **LogonId** field, present in both, is your link between them:

1. You get the **Image, User**, **LogonId** from the original Sysmon event (EventID=1)
2. Using **LogonId** field, you find the corresponding Logon event (EventID=4624)
3. You get the **LogonType** and **IpAddress** from the corresponding Logon event

With Splunk [subsearches(opens in new tab)](https://help.splunk.com/en/splunk-enterprise/get-started/search-tutorial/10.2/part-4-searching-the-tutorial-data/use-a-subsearch) and `join` keyword, you can correlate across multiple data sources within one search, and, for our example, build a unified tablecontaining both process and logon details:

![image.png](image.png)
