---
title: "hash function"
date: 2025-03-21 15:19:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "Hash functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to…"
media_subpath: /assets/img/tryhackme/2025-03-21-hash-function/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/hash/hash-function/
th_id: "cyber-101/cryptography-basics/hash/hash-function"
th_parent: "cyber-101/cryptography-basics/hash"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/hash"]
---

{% include tryhackme-nav.html %}

Hash functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to the input. Any slight change in the input data, even a single bit, should cause a significant change in the output.

The output of a hash function is typically raw bytes, which are then encoded. Common encodings are base64 or hexadecimal. `md5sum`, `sha1sum`, `sha256sum`, and `sha512sum` produce their outputs in hexadecimal format. Remember that hexadecimal format prints each raw byte as two hexadecimal digits.

**What’s a Hash Collision?**

A hash collision is when two different inputs give the same output. Because the number of inputs is practically unlimited and the number of possible outputs is limited, this leads to collisions are unavoidable. However, a good hash function ensures that the probability of a collision is negligible.

MD5 and SHA1 have been attacked and are now considered insecure due to the ability to engineer hash collisions. Due to these, you shouldn’t trust either algorithm for hashing passwords or data.
