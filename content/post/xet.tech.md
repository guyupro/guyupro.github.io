---
title: "有趣的小鹅通"
date: 2021-09-13
tags: ["crack"]
draft: false
---

最近购买了个9.9元的课程，由于时间紧张就没来得及看，老师又限时打算把视频下架，那就只好先下载下来了。

打开网页看视频，看到是小鹅通平台的，试了试现有的现在工具，却无法使用，接下来只好手撸了。

之前的小鹅通视频可以直接chrome调试，找到m3u8的链接，然后使用m3u8下载工具[N_m3u8DL-CLI](https://github.com/nilaoda/N_m3u8DL-CLI)下载（如何使用请访问N_m3u8DL-CLI项目页）。


这次要下载的4个视频，总共有三种格式，获取m3u8链接地址的方式如下：

### 1.
链接地址

`https://encrypt-k-vod.xet.tech/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/drm/v.f(6位数字).ts?start=数字&end=数字&type=mpegts&exper=0&sign=cccccccccccccccccccccccccccccccc&t=dddddddd&us=eeeeeeeeeeee`


打开chrome按F12，搜索.ts 即可找到链接地址，随便选一个复制出来

去掉start去掉end，ts换成m3u8即可

`https://encrypt-k-vod.xet.tech/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/drm/v.f(6位数字).m3u8?type=mpegts&exper=0&sign=cccccccccccccccccccccccccccccccc&t=dddddddd&us=eeeeeeeeeeee`

### 2.
链接地址

`https://encrypt-k-vod.xet.tech/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/drm/v.f(6位数字)_数字.ts?type=mpegts&exper=0&sign=cccccccccccccccccccccccccccccccc&t=dddddddd&us=eeeeeeeeeeee`

去掉`_数字`，ts换成m3u8即可

`https://encrypt-k-vod.xet.tech/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/drm/v.f(6位数字).m3u8?type=mpegts&exper=0&sign=cccccccccccccccccccccccccccccccc&t=dddddddd&us=eeeeeeeeeeee`

### 3.
链接地址

`https://(10位数字).vod2.myqcloud.com/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/v.f(6位数字)_数字.ts`

同理，去掉`_数字`，ts换成m3u8即可

`https://encrypt-k-vod.xet.tech/xxxxxxxxxxxxxxxxxxxxxxxxxxxx/bbbbbbbbbbbbbbbbbbbbbbbbbbb/drm/v.f(6位数字).m3u8`