---
title: "Filtering"
date: 2025-08-29 08:00:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: "The rename(opens in new tab) command allows you to change the name of a field in your search results. This can help improve the readability of your search re…"
media_subpath: /assets/img/tryhackme/2025-08-29-filtering/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/splunk-exploring-spl/filtering/
th_id: "soc-lv-2/advanced-splunk/splunk-exploring-spl/filtering"
th_parent: "soc-lv-2/advanced-splunk/splunk-exploring-spl"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/splunk-exploring-spl"]
---

{% include tryhackme-nav.html %}

- fields :
- dedup : removes duplicate values from your search results.
- rename :

The [rename(opens in new tab)](https://help.splunk.com/en/splunk-enterprise/spl-search-reference/9.0/search-commands/rename) command allows you to change the name of a field in your search results. This can help improve the readability of your search results, especially if the original fields are too long or not suitable for showing them in the screenshots in formal SOC reports.

```c
index = windowslogs
| fields EventID User Image Hostname SourceIp
| rename User as Employee
```

The command is also useful to flatten JSON or XML subfields. For example, for a JSON log entry like `{"request": {"path": "/admin", "ip": "10.0.0.2"}}`, Splunk will create two fields: `request.path` and `request.ip`. If you don't want to type the prefix every time, consider removing it like in the example below:

```c
index=jsondata
| rename request.* as * // request.path -> path; request.ip -> ip
```

- regex : allows you to filter search results using regular expressions

```
index = windowslogs | regex Image = "\.exe$"
```
