---
title: "Digital Signatures and Certificate"
date: 2025-03-18 12:16:00 +0700
categories: ["TryHackMe", "Cyber 101", "Cryptography Basics"]
tags: ["tryhackme", "cryptography-basics"]
description: "Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Proving the authenticity of files means we know w…"
media_subpath: /assets/img/tryhackme/2025-03-18-digital-signatures-and-certificate/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/cryptography-basics/digital-signatures-and-certificate/
th_id: "cyber-101/cryptography-basics/digital-signatures-and-certificate"
th_parent: "cyber-101/cryptography-basics"
th_kind: note
th_order: 4
th_course: "cyber-101"
th_module: "cyber-101/cryptography-basics"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/cryptography-basics"]
---

{% include tryhackme-nav.html %}

Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Proving the authenticity of files means we know who created or modified them. Using asymmetric cryptography, you produce a signature with your private key, which can be verified using your public key. Only you should have access to your private key, which proves you signed the file. In many modern countries, digital and physical signatures have the same legal value.

**Quy trình ký số**:

1. Người tạo file **dùng private key** để tạo **digital signature** cho file.
2. Người nhận file sẽ **dùng public key** của người gửi để **xác minh chữ ký**.
3. Nếu xác minh thành công → chứng tỏ:
    - File này **do chính người giữ private key ký** → xác thực.
    - File **không bị thay đổi kể từ khi ký** → toàn vẹn.

![image.png](image.png)

### Về sự nhầm lẫn giữa **electronic signature** và **digital signature**

- **Electronic signature (chữ ký điện tử)**: đôi khi chỉ đơn giản là **dán ảnh chữ ký** vào file PDF hoặc Word.
    - Nhược điểm: **không đảm bảo tính toàn vẹn**. Ai cũng có thể **copy/paste** ảnh chữ ký đó → không chứng minh được file chưa bị sửa.
- **Digital signature (chữ ký số)**: dùng **private key** hoặc **certificate** để ký file.
    - Như vậy, nó **bảo vệ tính toàn vẹn** và chứng minh **nguồn gốc của file**.

> Tóm lại: “pasting an image” ≠ digital signature.
> 

In this task, we use the term *digital signature* to refer to signing a document using a private key or a certificate. This process is similar to the image shown above, where Bob encrypts a hash of his document and shares it with Alice, along with the original document. Alice can decrypt the encrypted hash and compare it with the hash of the file she received. This approach proves the document’s integrity, unlike pasting a fancy image of a signature.

## Certificates: Prove Who You Are!

Certificates are an essential application of public key cryptography, and they are also linked to digital signatures. A common place where they’re used is for HTTPS. How does your web browser know that the server you’re talking to is the real tryhackme.com?

The answer lies in certificates. The web server has a certificate that says it is the real tryhackme.com. The certificates have a chain of trust, starting with a root CA (Certificate Authority). From install time, your device, operating system, and web browser automatically trust various root CAs. Certificates are trusted only when the Root CAs say they trust the organisation that signed them. In a way, it is a chain; for example, the certificate is signed by an organisation, the organisation is trusted by a CA, and the CA is trusted by your browser. Therefore, your browser trusts the certificate. In general, there are long chains of trust. You can take a look at the certificate authorities trusted by Mozilla Firefox [here](https://wiki.mozilla.org/CA/Included_Certificates) and by Google Chrome [here](https://chromium.googlesource.com/chromium/src/+/main/net/data/ssl/chrome_root_store/root_store.md).

Let’s say you have a website and want to use HTTPS. This step requires having a TLS certificate. You can get one from the various certificate authorities for an annual fee. Furthermore, you can get your own TLS certificates for domains you own using [Let's Encrypt](https://letsencrypt.org/) for free. If you run a website, it’s worth setting up and switching to HTTPS, as any modern website would do.
