---
title: "Web Server Access Logs Analysis"
date: 2025-05-11 18:10:00 +0700
categories: ["TryHackMe", "Cyber 101", "Log Fundamental"]
tags: ["tryhackme", "log-fundamental"]
description: "The less command is helpful for handling multiple log files. You may need to analyze specific chunks one by one. For this, you can use the less command-line…"
media_subpath: /assets/img/tryhackme/2025-05-11-web-server-access-logs-analysis/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/log-fundamental/web-server-access-logs-analysis/
th_id: "cyber-101/log-fundamental/web-server-access-logs-analysis"
th_parent: "cyber-101/log-fundamental"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/log-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/log-fundamental"]
---

{% include tryhackme-nav.html %}

The `less` command is helpful for handling multiple log files. You may need to analyze specific chunks one by one. For this, you can use the less command-line utility, which helps you view one page at a time.

less command usage

```bash
root@kali$ less access.log
172.16.0.1 - - [06/Jun/2024:13:52:44] "GET /products HTTP/1.1" 404 "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
10.0.0.1 - - [06/Jun/2024:13:48:44] "GET /about HTTP/1.1" 404 "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
192.168.1.1 - - [06/Jun/2024:13:46:44] "GET /about HTTP/1.1" 200 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
:
```

Use `spacebar` to move to the next page and `b` to the previous page.

After running this command, the logs would be displayed in pages, one after one, making it easy for manual analysis. If you wish to search for something in the logs, you can type `/` followed by the pattern you are searching for and hit enter.

Use `n` to navigate to the next occurrence of your search and `N` to navigate to the previous occurrence of your search.
