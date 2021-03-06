---
layout: post
title: Stored Cross-Site Scripting via m1_name (Authenticated)
description: cve
summary: cve
tags: cve
---
# Stored Cross-Site Scripting via m1_name (Authenticated)
---
## Product Version
Vulnerability is present on the following version: 2.2.15 (CMS made simple)
![alt text](/assets/images/Pasted image 20211025202455.png)
<a href="/assets/versions/cmsms-2.2.15-install.zip" download>cmsms-2.2.15-install.zip</a>

![alt text](/assets/images/Pasted image 20211024150751.png)
All checks enabled at install phase.
## Proof of Concept
The following image will show a "dashboard" of a user with privileges:
![alt text](/assets/images/Pasted image 20211025203136.png)
Any user who can "Add category" or "Edit category" from "Site Admin" -> "Settings - News module" can trigger a stored cross site scripting vulnerability.
![alt text](/assets/images/Pasted image 20211025204422.png)
An attacker can update the name field to a xss payload such as:
```html
<script>alert("trigger")</script>
```

![alt text](/assets/images/Pasted image 20211025204446.png)
Submit Request (payload in m1_name):
![alt text](/assets/images/Pasted image 20211025221639.png)
Submit Response:
![alt text](/assets/images/Pasted image 20211025204841.png)
After following redirection:
![alt text](/assets/images/Pasted image 20211025204927.png)
![alt text](/assets/images/Pasted image 20211025204952.png)
![alt text](/assets/images/Pasted image 20211025205005.png)



## Trigger:
- View content -> news
![alt text](/assets/images/Pasted image 20211025205114.png)
Reflection of payload:
![alt text](/assets/images/Pasted image 20211025210253.png) 

-  View site (all pages) or preview site
![alt text](/assets/images/Pasted image 20211025205345.png)
![alt text](/assets/images/Pasted image 20211025205418.png)
![alt text](/assets/images/Pasted image 20211025205436.png)
![alt text](/assets/images/Pasted image 20211025205608.png)
All pages/articles can trigger this vulnerability

Reflection of payload in response:
![alt text](/assets/images/Pasted image 20211025210024.png)

We recommend to sanitize all user input from all parameters, especially "m1_name" from 
admin/moduleinterface.php




