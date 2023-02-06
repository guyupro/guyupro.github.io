---
title: "Windows远程桌面访问Kali Linux"
date: 2023-02-06
tags: ["kali","mstsc"]
draft: false
---

```bash
sudo apt-get purge tightvnc xrdp 
sudo apt-get install xfce4 tightvncserver xrdp 
sudo systemctl enable xrdp --now
```



![](https://www.guyu.pro/2023/02/06/1.webp)
![](https://www.guyu.pro/2023/02/06/2.webp)

