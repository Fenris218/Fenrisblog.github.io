---
title: "Burp Suite"
date: 2025-04-17 18:46:00 +0700
categories: ["TryHackMe", "Cyber 101", "Web Hacking"]
tags: ["tryhackme", "web-hacking"]
description: ""
media_subpath: /assets/img/tryhackme/2025-04-17-burp-suite/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/web-hacking/burp-suite/
th_id: "cyber-101/web-hacking/burp-suite"
th_parent: "cyber-101/web-hacking"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/web-hacking"
th_size: 2
th_ancestors: ["cyber-101", "cyber-101/web-hacking"]
---

{% include tryhackme-nav.html %}

- **Proxy**: It enables interception and modification of requests and responses while interacting with web applications.
- **Repeater**: [Repeater](https://tryhackme.com/room/burpsuiterepeater) allows for capturing, modifying, and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error (e.g., in SQLi - Structured Query Language Injection) or testing the functionality of an endpoint for vulnerabilities.
    1. **Sniper**: The Sniper attack type is the default and most commonly used option. It cycles through the payloads, inserting one payload at a time into each position defined in the request. Sniper attacks iterate through all the payloads in a linear fashion, allowing for precise and focused testing.
    2. **Battering ram**: The Battering ram attack type differs from Sniper in that it sends all payloads simultaneously, each payload inserted into its respective position. This attack type is useful when testing for race conditions or when payloads need to be sent concurrently.
    3. **Pitchfork**: The Pitchfork attack type enables the simultaneous testing of multiple positions with different payloads. It allows the tester to define multiple payload sets, each associated with a specific position in the request. Pitchfork attacks are effective when there are distinct parameters that need separate testing.
    4. **Cluster bomb**: The Cluster bomb attack type combines the Sniper and Pitchfork approaches. It performs a Sniper-like attack on each position but simultaneously tests all payloads from each set. This attack type is useful when multiple positions have different payloads, and we want to test them all together.
- **Intruder**: [Intruder](https://tryhackme.com/room/burpsuiteintruder) allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.  that allows for automated request modification and repetitive testing with variations in input values.
- **Decoder**:  It can decode captured information or encode payloads before sending them to the target.
- **Comparer**: As the name suggests, [Comparer](https://tryhackme.com/room/burpsuiteom) enables the comparison of two pieces of data at either the word or byte level.
- **Sequencer**: [Sequencer](https://tryhackme.com/room/burpsuiteom) is typically employed when assessing the randomness of tokens, such as session cookie values or other supposedly randomly generated data. If the algorithm used for generating these values lacks secure randomness, it can expose avenues for devastating attacks.

[Site map and Issue Definitions]({{ site.baseurl }}/tryhackme/cyber-101/web-hacking/burp-suite/site-map-and-issue-definitions/)

[Scoping and Targeting]({{ site.baseurl }}/tryhackme/cyber-101/web-hacking/burp-suite/scoping-and-targeting/)

