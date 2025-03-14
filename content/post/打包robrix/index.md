---
title: "打包robrix"
date: 2025-02-28T10:20:57+08:00
draft: false
author: "acyanbird"
summary: "打包robrix"
tags: ["rust", "makepad"]
---

官方下载确实没办法使用，因为 `libflac8` 无法使用。所以自己打包一下

寻找了一下命令，如果不管 debian 那边的标准，直接用
`ar r mypackage-42.deb debian-binary control.tar.gz data.tar.gz` 就可，尝试一下？