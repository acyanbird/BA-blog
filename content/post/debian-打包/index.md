---
title: "Debian 打包"
date: 2024-12-25T15:24:57+08:00
draft: true
author: "acyanbird"
summary: "Debian 打包"
tags: ["打包"]
---

总之先上一下[官方（看起来比较新）的教程](https://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.pdf)
![](image.png)

我们需要通过源代码包来构建 deb 包

### 获得源代码包

在 `/etc/apt/source.list` 里面把 src 的注释取消（看了就知道了）


### 实操练习环节 1：修改 grep 软件包

通过 `apt-get source grep` 获得源码包，然后通过 `dpkg-source -x grep_2.12-2.dsc` 解压