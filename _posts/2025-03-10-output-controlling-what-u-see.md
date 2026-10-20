---
title: "Output : controlling what u see"
date: 2025-03-10 16:08:00 +0700
categories: ["TryHackMe", "Cyber 101", "Nmap"]
tags: ["tryhackme", "nmap"]
description: "This task focuses on two main features:"
media_subpath: /assets/img/tryhackme/2025-03-10-output-controlling-what-u-see/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/nmap/output-controlling-what-u-see/
th_id: "cyber-101/nmap/output-controlling-what-u-see"
th_parent: "cyber-101/nmap"
th_kind: note
th_order: 5
th_course: "cyber-101"
th_module: "cyber-101/nmap"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/nmap"]
---

{% include tryhackme-nav.html %}

This task focuses on two main features:

- Showing additional information while a scan takes place
- Choosing the file format to save the scan report

Một vài lúc việc scan rất lâu, Nếu muốn xem real-time information about the scan progress: -v

Most likely, the `-v` option is more than enough for verbose output; however, if you are still unsatisfied, you can increase the verbosity level by adding another “v” such as `-vv` or even `-vvvv` 

If all this verbosity does not satisfy your needs, you must consider the `-d` for debugging-level output. Similarly, you can increase the debugging level by adding one or more “d” or by specifying the debugging level directly. The maximum level is `-d9`

**Saving Scan Report**

The three most useful are normal (human-friendly) output, XML output, and grepable output, in reference to the `grep` command. You can select the scan report format as follows:

- `oN <filename>` - Normal output
- `oX <filename>` - XML output
- `oG <filename>` - `grep`able output (useful for `grep` and `awk`)
- `oA <basename>` - Output in all major formats

![image.png](image.png)
