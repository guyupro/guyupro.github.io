---
title: "gvm安装Go 1.5"
date: 2015-08-27
tags: ["gvm", "go"]
draft: false
---


Go 1.5及更新版本使用Go 1.4进行构建，Go源码树完全消除所有C的代码。
 gvm项目地址：<https://github.com/moovweb/gvm>

1. 安装gvm

```
sudo apt-get install curl git mercurial make binutils bison gcc build-essential
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

2. 然后安装Go 1.4

```
gvm install go1.4
gvm use go1.4
export GOROOT_BOOTSTRAP=$GOROOT
```

3. 最后安装Go 1.5

```
gvm install go1.5
gvm use go1.5
```

执行 `go version` 即可查看到版本号，已经安装并使用了go 1.5