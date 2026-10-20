---
title: "Linux Shells"
date: 2025-01-09 16:08:00 +0700
categories: ["TryHackMe", "Cyber 101", "Linux fundamental"]
tags: ["tryhackme", "linux-fundamental"]
description: ""
media_subpath: /assets/img/tryhackme/2025-01-09-linux-shells/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/linux-fundamental/linux-shells/
th_id: "cyber-101/linux-fundamental/linux-shells"
th_parent: "cyber-101/linux-fundamental"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/linux-fundamental"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/linux-fundamental"]
---

{% include tryhackme-nav.html %}

## 1. Shell scripting

- Loops :

```bash
## Defining the Interpreter 
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

- conditions :

```bash
## Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```

- Lưu ý :
    - sau if phải có “; then”
    - kết thúc if phải có fi
    - phải có khoảng trắng trong “ [ ] “
    - phải có khoảng trắng sau echo “

## 2. The locker Script
