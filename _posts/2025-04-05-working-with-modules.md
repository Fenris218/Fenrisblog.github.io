---
title: "Working with modules"
date: 2025-04-05 18:34:00 +0700
categories: ["TryHackMe", "Cyber 101", "Metasploit"]
tags: ["tryhackme", "metasploit"]
description: "All parameters are set using the same command syntax:"
media_subpath: /assets/img/tryhackme/2025-04-05-working-with-modules/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/metasploit/working-with-modules/
th_id: "cyber-101/metasploit/working-with-modules"
th_parent: "cyber-101/metasploit"
th_kind: note
th_order: 3
th_course: "cyber-101"
th_module: "cyber-101/metasploit"
th_size: 0
th_ancestors: ["cyber-101", "cyber-101/metasploit"]
---

{% include tryhackme-nav.html %}

All parameters are set using the same command syntax:

```
set PARAMETER_NAME VALUE
```

Once you have set a parameter, you can use the `show options` command to check the value was set correctly.

![image.png](image.png)

You can override any set parameter using the set command again with a different value. You can also clear any parameter value using the `unset` command or clear all set parameters with the `unset all` command.

![image.png](image%201.png)

You can use the `setg` command to set values that will be used for all modules. The `setg` command is used like the set command. The difference is that if you use the `set` command to set a value using a module and you switch to another module, you will need to set the value again. The `setg` command allows you to set the value so it can be used by default across different modules. You can clear any value set with `setg` using `unsetg`.

![image.png](image%202.png)

## **Using modules**

Once all module parameters are set, you can launch the module using the `exploit` command.

The `exploit` command can be used without any parameters or using the “`-z`” parameter.

The `exploit -z` command will run the exploit and background the session as soon as it opens.

![image.png](image%203.png)

## **Sessions**

Once a vulnerability has been successfully exploited, a session will be created. This is the communication channel established between the target system and Metasploit.

You can use the `background` command to background the session prompt and go back to the msfconsole prompt. = Khi bạn đang ở trong session, nhưng bạn không muốn thoát session, chỉ muốn **quay lại msfconsole** để chạy lệnh khác → thì bạn dùng:

![image.png](image%204.png)

Alternatively, `CTRL+Z` can be used to background sessions.
The `sessions` command can be used from the msfconsole prompt or any context to see the existing sessions.

![image.png](image%205.png)

To interact with any session, you can use the `sessions -i` command followed by the desired session number.

![image.png](image%206.png)
