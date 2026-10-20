---
title: "Phising prevention"
date: 2025-08-03 18:34:00 +0700
categories: ["TryHackMe", "SOC LV1", "Phising prevention"]
tags: ["tryhackme", "phising-prevention"]
description: "SPF is used to authenticate the sender of an email. With an SPF record in place, ISP can verify that a mail server is authorized to send email for a specific…"
media_subpath: /assets/img/tryhackme/2025-08-03-phising-prevention/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv1/phising-prevention/
th_id: "soc-lv1/phising-prevention"
th_parent: "soc-lv1"
th_kind: module
th_order: 20
th_course: "soc-lv1"
th_module: "soc-lv1/phising-prevention"
th_size: 0
th_ancestors: ["soc-lv1"]
---

{% include tryhackme-nav.html %}

## 1. Sender Policy Framework (SPF)

SPF is used to authenticate the sender of an email. With an SPF record in place, ISP can verify that a mail server is authorized to send email for a specific domain . An SPF record is a DNS TXT record containing a list of IP address that are allowed to send email on behalf of your domain.

So, in essence, when an email is sent, the receiving mail server checks the domain's SPF record to verify whether the sending server is authorized to send messages on behalf of that domain. The delivery of the email (intended action) is based on the result of the SPF record verification.

![image.png](image.png)

| **Verification Result** | **Intended Action** |
| --- | --- |
| Pass, Neutral, None | Accept (Allow and process the email) |
| SoftFail, PermError | Flag (Mark as suspicious but allow) |
| Fail, TempError | Reject (Immediately discard the email) |

### **SPF Records**

Let's take a look at a sample SPF record and break down its format. Further information on SPF Record Syntax can be found [here(opens in new tab)](https://dmarcian.com/spf-syntax-table/).

`v=spf1 ip4:127.0.0.1 include:_spf.google.com -all`

- `v=spf1` Signifies the start of the SPF record
- `ip4:127.0.0.1` Specifies which IP can send mail (IPv4 in this case)
- `include:_spf.google.com` Specifies which domain can send mail
- `all` Non-authorized emails will be rejected

### **Tools**

The [**SPF Surveyor(opens in new tab)](https://dmarcian.com/spf-survey/) and Google Admin Toolbox [Messageheader**(opens in new tab)](https://toolbox.googleapps.com/apps/messageheader/)

## 2. DomainKeys Identified Mail (DKIM)

DKIM is used for the authentication of an email that’s being sent. Like SPF, DKIM is an open standard for email authentication that is used for DMARC alignment. A DKIM record exists in the DNS, but it is more complex than SPF. DKIM’s advantage is that it can survive forwarding, which makes it superior to SPF and a foundation for securing your email.

![image.png](image%201.png)

### **DKIM Records**

Here is a sample DKIM record, along with its components.

`v=DKIM1; k=rsa; p=<public_key>`

- `v=DKIM1` Specifies the version of DKIM being used (optional)
- `k=rsa` The key type. The  encryption algorithm is standard
    
    RSA
    
- `p=` This is the public key that will be matched to the private key to verify the DKIM signature

## 3. **Domain-Based Message Authentication, Reporting, and Conformance (DMARC)**

DMARC, an open source standard, uses a concept called alignment to tie the result of two other open source standards,  SPF (a published list of servers that are authorized to send email on behalf of a domain) and DKIM (a tamper-evident domain seal associated with a piece of email), to the content of an email.

This means that DMARC ensures the sender's domain matches the domains verified by SPF and DKIM

This means that DMARC ensures the sender's domain matches the domains verified by SPF and DKIM. If the alignment fails, DMARC instructs the recipient server on how to handle the email based on a policy specified in the record.

## 4. Secure/Multipurpose internet Mail Extensions (S/MIME)

**Secure/Multipurpose Internet Mail Extensions** ([**S/MIME**(opens in new tab)](https://learn.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo)) is a standard protocol for sending digitally signed and encrypted messages. It is based on public key cryptography, where the private key is never shared and the public key can be distributed openly. The two main components and security features of S/MIME are:

**Digital Signature**

The sender signs the message with their private key, the recepient verifies the sender's identity using the sender's public key. This security feature provides:

- **Authentication**: Confirms the sender's identity through their digital certificate
- **Non-repudiation**: Ensures the sender cannot deny sending the message
- **Data Integrity**: Detects any changes to the message after it's signed

**Encryption**

The sender encrypts the message using the recipient's public key, allowing only the recipient to decrypt it with their private key. This security feature provides:

- **Confidentiality**: Keeps the content private and readable only by the intended recipient

### **S/MIME Example**

- Bob wishes to securely send the email with S/ to Mary
    
    MIME
    
- Bob creates a digital certificate to generate the **Digital Signature**
- Bob "signs" the email message with his private key (**Digital Signature**)
- Bob openly shares his public key with Mary (**Digital Signature**)
- Bob also asks the public key of Mary to encrypt the email (**Encryption**)
- Mary verifies Bob's message with Bob's public key (**Digital Signature**)
- Mary decrypts the received message with her private key (**Encryption**)
- To send a reply email, Mary performs the same procedure from the start
- Both Bob and Mary will now have each other's certificates for future correspondence
