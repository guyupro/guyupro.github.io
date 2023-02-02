---
title: "Let's Encrypt 通配符证书"
date: 2021-10-22
tags: ["https"]
draft: false
---

## 验证DNS txt记录 

安装`certbot-auto`，我这里使用[Ubuntu 20.04](https://certbot.eff.org/lets-encrypt/ubuntufocal-other) 进行安装。

使用Certbot的手动模式向Let's Encrypt 申请证书

首次申请
`sudo certbot certonly --manual --preferred-challenges=dns-01`

到期续约
`sudo certbot --manual --preferred-challenges dns certonly`

需要注意填写域名时格式为`,`分割，例如`xx.com,*.xx.com`

## 使用Cloudflare api

配置文件`/etc/letsencrypt/cloudflare.ini`

```
dns_cloudflare_email = i@guyu.pro
dns_cloudflare_api_key = 0gatv76ctf86yzdcxw4o9obd9f91z4lo5a6fa
```
