---
title: "transforming commands"
date: 2025-08-31 10:02:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: "Transforming commands(opens in new tab) allow you to change raw event data into useful summaries, statistics, and visualizations."
media_subpath: /assets/img/tryhackme/2025-08-31-transforming-commands/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/splunk-exploring-spl/transforming-commands/
th_id: "soc-lv-2/advanced-splunk/splunk-exploring-spl/transforming-commands"
th_parent: "soc-lv-2/advanced-splunk/splunk-exploring-spl"
th_kind: note
th_order: 3
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/splunk-exploring-spl"]
---

{% include tryhackme-nav.html %}

[Transforming commands(opens in new tab)](https://help.splunk.com/en/splunk-cloud-platform/search/search-manual/10.0.2503/create-statistical-tables-and-chart-visualizations/about-transforming-commands-and-searches) allow you to change raw event data into useful summaries, statistics, and visualizations. 

## **General Transformational Commands**

| **Command** | **Example** | **Explanation** |
| --- | --- | --- |
| top | `index=windowslogs | top User limit=5` | Returns the ten most frequent values of the field specified. A numerical value can be included with `limit=` to reduce or expand the results |
| rare | `index=windowslogs | rare User limit=5` | Returns the ten least frequent values of the field specified. A numerical value can be included with `limit=` to reduce or |
- hightlight

```
index=windowslogs | highlight User EventID Image "Process accessed"
```

- **Stats**

| **Command Function** | **Example** | **Explanation** |
| --- | --- | --- |
| Average | `stats avg(ProcessCount)` | Calculates the average value of the chosen field |
| Max | `stats max(Price)` | Returns the maximum value of the chosen field |
| Min | `stats min(UserAge)` | Returns the minimum value of the chosen field |
| Sum | `stats sum(Cost)` | Returns the sum of the chosen field values |
| Count | `stats count by SourceIp` | Returns the number of occurrences of the chosen field |
- lookup :

Similarly, [lookup(opens in new tab)](https://help.splunk.com/en/splunk-enterprise/spl-search-reference/9.0/search-commands/lookup) is used to enrich events using external data sources. It matches a field in your search to a corresponding field in a `CSV` file or lookup table. In this example, a `CSV` was created that associates the `Hostname` field with an employee role signified by `UserRole`.

```
index=windowslogs
| lookup user_roles Hostname OUTPUT UserRole
| stats count by Hostname UserRole

```

![image.png](image.png)
