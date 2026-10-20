---
title: "Other configuration files"
date: 2025-09-05 15:07:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Advanced Splunk"]
tags: ["tryhackme", "advanced-splunk"]
description: ""
media_subpath: /assets/img/tryhackme/2025-09-05-other-configuration-files/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/advanced-splunk/data-manipulation/other-configuration-files/
th_id: "soc-lv-2/advanced-splunk/data-manipulation/other-configuration-files"
th_parent: "soc-lv-2/advanced-splunk/data-manipulation"
th_kind: note
th_order: 2
th_course: "soc-lv-2"
th_module: "soc-lv-2/advanced-splunk"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/advanced-splunk", "soc-lv-2/advanced-splunk/data-manipulation"]
---

{% include tryhackme-nav.html %}

- transforms.conf :  Allows you to define data transformations and enrichments on indexed events

```
[extract_username]
REGEX = User\s+(\S+)\s+logged
FORMAT = username::$1
```

- fields.conf : Defines how custom or extracted fields behave in Splunk,  **Example:** Below, `fields.conf` references the `transforms.conf` entry by specifying how to handle our new `username` field

```
[username]
INDEXED = true

```

- indexes.conf : Manages the configuration of indexes in Splunk, including storage, retention policies, and access control

```
[my_index]
homePath = $SPLUNK_DB/my_index/db
coldPath = $SPLUNK_DB/my_index/colddb
thawedPath = $SPLUNK_DB/my_index/thaweddb
maxTotalDataSizeMB = 100000
```

- outputs.conf : pecifies the destination and settings for sending indexed data to various outputs, such as remote Splunk instances or third-party systems
