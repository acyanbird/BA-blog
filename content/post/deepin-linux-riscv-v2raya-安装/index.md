---
title: "Deepin Linux Riscv V2raya 安装"
date: 2025-01-03T11:00:30+08:00
draft: false
author: "acyanbird"
summary: "Deepin Linux Riscv V2raya 安装"
tags: ["v2ray"]
---

这个和x64版本不太一样，installer 里面并没有自带 v2ray-core，所以要两个分别放

首先下载 [v2raya](https://github.com/v2rayA/v2rayA/releases)，然后是 [xray](https://github.com/XTLS/Xray-core/releases) ，之后使用 [xray-install](https://github.com/XTLS/Xray-install) 脚本，在 xray 的 README 里面。  
使用 `sudo bash install-release.sh help` 查看一下，就有安装本地文件的选项 -l，当然你也可以顺手带上 geoip.dat 和 geosite.dat，大概在 `/usr/local/share/xray` 这里

