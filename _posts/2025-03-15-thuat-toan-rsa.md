---
title: "Thuật toán RSA"
date: 2025-03-15 09:13:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "RSA is based on the mathematically difficult problem of factoring a large number. Multiplying two large prime numbers is a straightforward operation; however…"
media_subpath: /assets/img/tryhackme/2025-03-15-thuat-toan-rsa/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/types-of-encryption/asymmetric/thuat-toan-rsa/
th_id: "cyber-101/cryptography-basics/types-of-encryption/asymmetric/thuat-toan-rsa"
th_parent: "cyber-101/cryptography-basics/types-of-encryption/asymmetric"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/types-of-encryption", "cyber-101/cryptography-basics/types-of-encryption/asymmetric"]
---

{% include tryhackme-nav.html %}

### The Math That Makes RSA Secure

RSA is based on the mathematically difficult problem of factoring a large number. Multiplying two large prime numbers is a straightforward operation; however, finding the factors of a huge number takes much more computing power.

It’s simple to multiply two prime numbers together even on paper, say 113 × 127 = 14351. Even for larger prime numbers, it would still be a feasible job, even by hand. Consider the following numeric example:

- Prime number 1: 982451653031
- Prime number 2: 169743212279
- Their product: 982451653031 × 169743212279 = 166764499494295486767649

On the other hand, it’s pretty tricky to determine what two prime numbers multiply together to make 14351 and even more challenging to find the factors of 166764499494295486767649.

In real-world examples, the prime numbers would be much bigger than the ones in this example. A computer can easily factorise 166764499494295486767649; however, it cannot factorise a number with more than 600 digits. And you would agree that the multiplication of the two huge prime numbers, each around 300 digits, would be easier than the factorisation of their product.

### Numerical Example

Let’s revisit encryption, decryption, and key usage in asymmetric encryption. The public key is known to all correspondents and is used for encryption, while the private key is protected and used for decryption, as shown in the figure below.

![Alice encrypts the message with Bob's public key and Bob decrypts it with his private key.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1725294065881.svg)

In the [Cryptography Basics](https://tryhackme.com/r/room/cryptographybasics) room, we explained the modulo operation and said it plays a significant role in cryptography. In the following simplified numerical example, we see the RSA algorithm in action:

1. Bob chooses two prime numbers: *p* = 157 and *q* = 199. He calculates *n* = *p* × *q* = 31243.
2. With *ϕ*(*n*) = *n* − *p* − *q* + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects *e* = 163 such that *e* is relatively prime to *ϕ*(*n*); moreover, he selects *d* = 379, where *e* × *d* = 1 mod *ϕ*(*n*), i.e., *e* × *d* = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (*n*,*e*), i.e., (31243,163) and the private key is $(n,d), i.e., (31243,379).
3. Let’s say that the value they want to encrypt is *x* = 13, then Alice would calculate and send *y* = *x* mod *n* = 13 mod 31243 = 16341.
    
    *e*
    
    163
    
4. Bob will decrypt the received value by calculating *x* = *y* mod *n* = 16341 mod 31243 = 13. This way, Bob recovers the value that Alice sent.
    
    *d*
    
    379
