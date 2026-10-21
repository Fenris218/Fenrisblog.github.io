---
title: "Active Directory Basics"
date: 2025-01-03 10:02:00 +0700
categories: ["TryHackMe", "Cyber 101", "Window Fundamental"]
tags: ["tryhackme", "window-fundamental"]
description: ""
media_subpath: /assets/img/tryhackme/2025-01-03-active-directory-basics/
toc: true
comments: false
hidden: true
permalink: /tryhackme/cyber-101/window-fundamental/active-directory-basics/
th_id: "cyber-101/window-fundamental/active-directory-basics"
th_parent: "cyber-101/window-fundamental"
th_kind: note
th_order: 1
th_course: "cyber-101"
th_module: "cyber-101/window-fundamental"
th_size: 2
th_ancestors: ["cyber-101", "cyber-101/window-fundamental"]
---

{% include tryhackme-nav.html %}

- **Active Directory (AD) :  is a single repository to centralise the administration of common components of a Windows computer network**
- **Windows domain  : is a group of users and computers under the administration of a given business.**
- Domain Controller (DC) **: is The server that runs the Active Directory services**
- The main advantages of having a configured Windows domain are:
    - **Centralised identity management:**
    - **Managing security policies:**
- OU (Organizational Unit) là một **đơn vị tổ chức** trong **Active Directory (AD)** — dùng để **chia nhỏ domain** thành các phần hợp lý hơn để **quản lý người dùng, máy tính, nhóm và chính sách (GPO)**.
- ADSI Edit cho phép bạn chỉnh *từng thuộc tính sâu bên trong đối tượng AD*.
- **AD DS** : is the core of any Windows Domain , this service acts as a catalogue that holds the information of all of the "objects" that exist on your network, such as :
    - Users : are one of the objects known as **security principals,  a security principal is an object that can act upon resources in the network. Users can be used to represent two types of entities:**
        - People
        - **Services:** you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service. ( là tài khoản dùng để chạy các dịch vụ )
    - Machine :   every computer that joins the Active Directory domain, a machine object will be created. Machines are also considered "security principals" and are assigned an account just as any regular user. This account has somewhat limited rights within the domain itself. The machine accounts themselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in. The machine account name is the computer's name followed by a dollar sign. For example, a machine named `DC01` will have a machine account called `DC01$`.
    - Security Groups :
        - you can define user groups to assign access rights to files or other resources to entire groups instead of single users. This allows for better manageability as you can add users to an existing group, and they will automatically inherit all of the group's privileges. Security groups are also considered security principals and, therefore, can have privileges over resources on the network.
        - Groups can have both users and machines as members. If needed, groups can include other groups as well.
        - Several groups are created by default in a domain
        
- **security groups vs OUs:** You are probably wondering why we have both groups and OUs. While both are used to classify users and computers, their purposes are entirely different:
    - **OUs** are handy for **applying policies** to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user.
    - **Security Groups**, on the other hand, are used to **grant permissions over resources**. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be a part of many groups, which is needed to grant access to multiple resources.

![image.png](image.png)

- Delegattion (ủy quyền) : is to give specific users some control over some OUs. this process allows you to grant users specific privileges to perform advance tasks on OUs without needing a Domain Adminstator to step in
- Managing Computers in AD: By default, all the machines that join a domain (except for the DCs) will be put in the container called "Computers”
- GPO : GPOs are simply a collection of settings that can be applied to OUs
- Authentication:
    - When using Windows domains, all credentials are stored in the Domain Controllers. Whenever a user tries to authenticate to a service using domain credentials, the service will need to ask the Domain Controller to verify if they are correct. Two protocols can be used for network authentication in windows domains:
        - **Kerberos:** Used by any recent version of Windows. This is the default protocol in any recent domain.
        - **NetNTLM:** Legacy authentication protocol kept for compatibility purposes.
    
    [**Kerberos Authentication**]({{ site.baseurl }}/tryhackme/cyber-101/window-fundamental/active-directory-basics/kerberos-authentication/)
    
- 

