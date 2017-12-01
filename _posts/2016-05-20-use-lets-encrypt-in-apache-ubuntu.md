---
layout: post
title: Use Let's Encrypt in Apache/Ubuntu
date: 2016-05-20 20:00:00 -0300
categories: ssl linux apache ubuntu
---

It's a matter of time until hosting providers offer HTTPS on theirs VPS with Let's Encrypt certificates with a single click, until then...

Install the Let’s Encrypt client:

```shell
$ sudo git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
```

Request the certificate(s). For multiple domains use as many `-d domain-name` as needed:

```shell
$ /opt/letsencrypt/letsencrypt-auto --apache -d example.com -d www.example.com
```

Let’s Encrypt certificates are valid for 90 days, and you can automate the renewal process using crontab:

```shell
$ sudo crontab -e
```

As the process won't do anything until the certificates are due for renewal, let's schedule it once a week (tuesdays at 1 am):

```shell
0 1 * * 2 /opt/letsencrypt/letsencrypt-auto renew >> /var/log/letsencrypt.log
```
