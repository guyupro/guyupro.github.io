---
title: "PVE Guest Agent未运行"
date: 2023-09-12
tags: ["pve"]
draft: false
---

参考：<https://pve.proxmox.com/wiki/Qemu-guest-agent>

## Linux

### Debian/Ubuntu

```bash
apt-get install qemu-guest-agent
```

### Redhat 

```bash
yum install qemu-guest-agent
```

## Windows

下载<https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers>  安装即可。
