---
title: "Security Headers"
date: 2025-04-15 16:44:00 +0700
categories: ["TryHackMe", "Cyber 101", "Web Hacking"]
tags: ["tryhackme", "web-hacking"]
description: "HTTP Security Headers help improve the overall security of the web application by providing mitigations against attacks like Cross-Site Scripting (XSS), clic…"
media_subpath: /assets/img/tryhackme/2025-04-15-security-headers/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/web-hacking/web-application-basics/security-headers/
th_id: "cyber-101/web-hacking/web-application-basics/security-headers"
th_parent: "cyber-101/web-hacking/web-application-basics"
th_kind: note
th_order: 2
th_course: "cyber-101"
th_module: "cyber-101/web-hacking"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/web-hacking", "cyber-101/web-hacking/web-application-basics"]
---

{% include tryhackme-nav.html %}

HTTP Security Headers help improve the overall security of the web application by providing mitigations against attacks like Cross-Site Scripting (XSS), clickjacking, and others. We will now dig deeper into the following security headers:

- Content-Security-Policy (CSP)
- Strict-Transport-Security (HSTS)
- X-Content-Type-Options
- Referrer-Policy

You can use a site like [https://securityheaders.io/](https://securityheaders.io/) to analyse the security headers of any website. After the discussion in this task, you will hopefully have a better understanding of what it is reporting on.

## **Content-Security-Policy (CSP)**

A CSP header is an additional security layer that can help mitigate against common attacks like Cross-Site Scripting (XSS). Malicious code could be hosted on a separate website or domain and injected into the vulnerable website. A CSP provides a way for administrators to say what domains or sources are considered safe and provides a layer of mitigation to such attacks.

example CSP header:

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

- **default-src:** which specifies the default policy of self, which means only the current website.
- **script-src:** which specifics the policy for where scripts can be loaded from, which is self along with scripts hosted on `https://cdn.tryhackme.com`
- **style-src:** which specifies the policy for where style CSS style sheets can be loaded from the current website (self)

## Strict-Transport-Security (HSTS)

The HSTS header ensures that web browsers will always connect over HTTPS.

an example of HSTS: 

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

## X-Content-Type-Options

The X-Content-Type-Options header can be used to instruct browsers not to guess the MIME time of a resource but only use the Content-Type header. Here’s an example:

`X-Content-Type-Options: nosniff`

Here’s a breakdown of the X-Content-Type-Options header by directives:

- **nosniff**This directive instructs the browser not to sniff or guess the MIME type.

## Referrer-Policy

This header controls the amount of information sent to the destination web server when a user is redirected from the source web server, such as when they click a hyperlink. The header is available to allow a web administrator to control what information is shared.  Here are some examples of Referrer-Policy:

- `Referrer-Policy: no-referrer`
- `Referrer-Policy: same-origin`
- `Referrer-Policy: strict-origin`
- `Referrer-Policy: strict-origin-when-cross-origin`

Here’s a breakdown of the Referrer-Policy header by directives:

- **no-referrer**This completely disables any information being sent about the referrer
- **same-origin**This policy will only send referrer information when the destination is part of the same origin. This is helpful when you want referrer information passed when hyperlinks are within the same website but not outside to external websites.
- **strict-origin**This policy only sends the referrer as the origin when the protocol stays the same. So, a referrer is sent when an HTTPS connection goes to another HTTPS connection.
- **strict-origin-when-cross-origin**This is similar to strict-origin except for same-origin requests, where it sends the full URL path in the origin header.
