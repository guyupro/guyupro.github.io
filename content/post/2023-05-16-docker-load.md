---
title: "docker内网"
date: 2023-05-16
tags: ["docker"]
draft: false
---

A 机


```bash
docker  pull ubuntu:22.04
docker save ubuntu:22.04 >ubuntu22.04.tar

```

B机

```bash
type  ubuntu22.04.tar |docker load
```
