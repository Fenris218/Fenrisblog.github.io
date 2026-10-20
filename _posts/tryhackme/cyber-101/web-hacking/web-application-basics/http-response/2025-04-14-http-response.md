---
title: "HTTP Response"
date: 2025-04-14 15:43:00 +0700
categories: ["TryHackMe", "Cyber 101", "Web Hacking"]
tags: ["tryhackme", "web-hacking"]
description: "The first line in every HTTP response is called the Status Line. It gives you three key pieces of info:"
media_subpath: /assets/img/tryhackme/2025-04-14-http-response/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/web-hacking/web-application-basics/http-response/
th_id: "cyber-101/web-hacking/web-application-basics/http-response"
th_parent: "cyber-101/web-hacking/web-application-basics"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/web-hacking"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/web-hacking", "cyber-101/web-hacking/web-application-basics"]
---

{% include tryhackme-nav.html %}

## Status Line

The first line in every HTTP response is called the **Status Line**. It gives you three key pieces of info:

1. **HTTP Version**: This tells you which version of HTTP is being used.
2. **Status Code**: A three-digit number showing the outcome of your request.
3. **Reason Phrase**: A short message explaining the status code in human-readable terms.

#### Status Codes and Reason Phrases

**Informational Responses (100-199)**

These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.

**Successful Responses (200-299)**

These codes mean everything worked as expected. The server processed the request and sent back the requested data.

**Redirection Messages (300-399)**

These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.

**Client Error Responses (400-499)**

These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.

**Server Error Responses (500-599)**

These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.

## Header

When a web server responds to an HTTP request, it includes **HTTP response headers**, which are basically key-value pairs. These headers provide important info about the response and tell the client (usually the browser) how to handle it.

![image.png](image.png)

#### **Required Response Headers**

- **Date**:
    
    Example: `Date: Fri, 23 Aug 2024 10:43:21 GMT`
    
- **Content-Type**:
    
    Example: `Content-Type: text/html; charset=utf-8`
    
- **Server**:
    
    Example: `Server: nginx`
    
    This header shows what kind of server software is handling the request. It’s good for debugging, but it can also reveal server information that might be useful for attackers, so many people remove or obscure this one.
    

#### **Other Common Response Headers**

Besides the essential ones, there are other common headers that give additional instructions to the client or browser and help control how the response should be handled.

- **Set-Cookie**:
    
    Example: `Set-Cookie: sessionId=38af1337es7a8`
    
    This one sends cookies from the server to the client, which the client then stores and sends back with future requests. To keep things secure, make sure cookies are set with the `HttpOnly` flag (so they can’t be accessed by JavaScript) and the `Secure` flag (so they’re only sent over HTTPS).
    
- **Cache-Control**:
    
    Example: `Cache-Control: max-age=600`
    
    This header tells the client how long it can cache the response before checking with the server again. It can also prevent sensitive info from being cached if needed (using `no-cache`).
    
- **Location**:
    
    Example: `Location: /index.html`
    
    This one’s used in redirection (3xx) responses. It tells the client where to go next if the resource has moved
