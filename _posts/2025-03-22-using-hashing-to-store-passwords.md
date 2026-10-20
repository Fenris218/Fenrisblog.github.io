---
title: "Using Hashing to Store Passwords"
date: 2025-03-22 16:20:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "instead of storing the password, you just stored its hash value using a secure hashing function."
media_subpath: /assets/img/tryhackme/2025-03-22-using-hashing-to-store-passwords/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/hash/using-hashing-to-store-passwords/
th_id: "cyber-101/cryptography-basics/hash/using-hashing-to-store-passwords"
th_parent: "cyber-101/cryptography-basics/hash"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics", "cyber-101/cryptography-basics/hash"]
---

{% include tryhackme-nav.html %}

instead of storing the password, you just stored its hash value using a secure hashing function. 

There’s just one problem with this. What if two users have the same password? As a hash function will always turn the same input into the same output, you will store the same password hash for each user. That means if someone cracks that hash, they gain access to more than one account. It also means someone can create a Rainbow Table to break the hashes.

A **Rainbow Table** is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash. A rainbow table trades the time to crack a hash for hard disk space, but it takes time to create. Here’s a quick example to get an idea of what a rainbow table looks like

![image.png](image.png)

Websites like [CrackStation](https://crackstation.net/) and [Hashes.com](https://hashes.com/en/decrypt/hash) internally use massive rainbow tables to provide fast password cracking for **hashes without salts**. Doing a lookup in a sorted list of hashes is quicker than trying to crack the hash.

![image.png](image%201.png)

### Protecting Against Rainbow Tables

To protect against rainbow tables, we add a salt to the passwords. The salt is a randomly generated value stored in the database and should be unique to each user. In theory, you could use the same salt for all users, but duplicate passwords would still have the same hash and a rainbow table could still be created for passwords with that salt.

The salt is added to either the start or the end of the password before it’s hashed, and this means that every user will have a different password hash even if they have the same password. Hash functions like Bcrypt and Scrypt handle this automatically. Salts don’t need to be kept private.
