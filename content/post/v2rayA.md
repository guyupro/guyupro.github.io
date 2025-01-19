---
title: "打靶环境之网络准备"
date: 0001-01-01
tags: ["v2raya"]
draft: false
---

在使用海外靶场时，例如 Proving Grounds Practice、HackTheBox等，用户可能会遇到网络连接失败或延迟过长的问题。这种情况通常是由于网络环境不佳或地理位置限制导致的。为了解决这些问题，使用 VPN 技术是一个有效的办法。在这里，我们以 [v2rayA](https://v2raya.org/)为例，进行演示。

## 服务端 Server

推荐<https://github.com/MHSanaei/3x-ui>配置。

- 可灵活配置梯子🪜

- 可配置socks5代理临时使用

## 客户端Client v2rayA

### 安装

在[Kali Linux](https://www.kali.org/)上安装

```bash
wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/keyrings/v2raya.asc
echo "deb [signed-by=/etc/apt/keyrings/v2raya.asc] https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list
sudo apt update
sudo apt install v2raya v2ray 
```

这里推荐使用socks5代理

```bash
sudo apt  -o Acquire::socks::proxy="socks5://127.0.0.1:1080/"  install v2raya v2ray
```
### 启动

```bash
sudo systemctl restart v2raya.service
```

### 配置

如 [http://localhost:2017](http://localhost:2017/) 访问UI，配置管理员用户名、密码。

#### 重置管理员密码

```bash
sudo v2raya --reset-password
```

### 导入节点

这里跟x-ui配置对的上就行。

### 设置

选择好节点，设置点击，选择。

| item                      | value               |
| ------------------------- | ------------------- |
| 透明代理/系统代理         | 启用:大陆白名单模式 |
| 透明代理/系统代理实现方式 | gvisor tun          |

```bash
curl ip.fm
```

查看是否获得节点IP。

------------

然后再拨号靶场的openvpn。
