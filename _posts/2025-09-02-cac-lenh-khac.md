---
title: "Các lệnh khác"
date: 2025-09-02 12:04:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: ""
media_subpath: /assets/img/tryhackme/2025-09-02-cac-lenh-khac/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/splunk-exploring-spl/cac-lenh-khac/
th_id: "soc-lv-2/advanced-splunk/splunk-exploring-spl/cac-lenh-khac"
th_parent: "soc-lv-2/advanced-splunk/splunk-exploring-spl"
th_kind: note
th_order: 5
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/splunk-exploring-spl"]
---

{% include tryhackme-nav.html %}

- eval : **tạo hoặc thay đổi field** dựa trên một biểu thức.
    - If : nếu đúng thì gán A không đúng thì gán B
    - like(Account_Name, "%$%") : kiểm tra `Account_Name` có chứa ký tự `$` hay không. ( % bất kì ký tự nào - SQL LIKE pattern)

```
| eval AccountType=if(like(Account_Name, "%$%"), "Computer Account", "User Account")

```

- bin : dùng để gom các timestamp vào từng khoảng thời gian

```
| bin _time span=1h
```

- khác với stats sẽ giảm số dòng, eventstats sẽ không giảm số dòng

```
| eventstats avg(hits) AS avg_hits
```

- stats dc() : dc là dùng để distint count

```
| stats dc(Service_Name) as targeted_services count by Account_Name, Client_Address
```

- lookup : Dùng table csv

```
| lookup asn_lookup network AS dstip OUTPUT dst_asn_org dst_category dst_risk
```
