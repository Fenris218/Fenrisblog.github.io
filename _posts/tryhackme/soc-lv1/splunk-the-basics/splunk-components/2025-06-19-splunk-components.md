---
title: "Splunk Components"
date: 2025-06-19 09:49:00 +0700
categories: ["TryHackMe", "SOC LV1", "Splunk: The Basics"]
tags: ["tryhackme", "splunk-the-basics"]
description: "Three main components: Forwarder, Indexer, and Search Head."
media_subpath: /assets/img/tryhackme/2025-06-19-splunk-components/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/splunk-the-basics/splunk-components/
th_id: "soc-lv1/splunk-the-basics/splunk-components"
th_parent: "soc-lv1/splunk-the-basics"
th_kind: note
th_order: 1
th_course: "soc-lv1"
th_module: "soc-lv1/splunk-the-basics"
th_size: 0
th_ancestors: ["soc-lv1", "soc-lv1/splunk-the-basics"]
---

{% include tryhackme-nav.html %}

Three main components: Forwarder, Indexer, and Search Head.

## **Splunk Forwarder**

Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored, and its main task is to collect the data and send it to the Splunk instance. It does not affect the endpoint's performance as it takes a few resources to process. 

![image.png](image.png)

The forwarder collects the data from the log sources and sends it to the Splunk Indexer. 

## **Splunk Indexer**

processing the data it receives from forwarders. It parses and normalizes the data into field-value pairs, categorizes it, and stores the results as events, making the processed data easy to search and analyze.

Now, the data, which is normalized and stored by the indexer, can be searched by the Search Head

## **Search Head**

is the place within the **Search & Reporting App** where users can search the indexed logs, as shown below. The searches are done using the **SPL** (Search Processing Language)

![image.png](image%201.png)
