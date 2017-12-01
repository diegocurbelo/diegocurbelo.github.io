---
layout: post
title:  Redirect HTTP to HTTPS in Apache
date:   2016-05-20 20:15:00 -0300
categories: ssl apache
---

Create a `.htaccess` file in the web server root with the following content to automatically redirects visitors to HTTPS

```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```
