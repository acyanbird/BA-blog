---
title: "Makepad101"
date: 2025-01-22T19:24:12+08:00
draft: false
author: "acyanbird"
summary: "Makepad101"
# tags: [""]
---

**为了入职加油！**
### 安装 makepad
clone 到 [rik分支](https://github.com/makepad/makepad/tree/rik)，直接按照 MacOS / PC 来安装就是了，下面的 Linux 是为了没有 X11 环境使用的……目前在 X11 可以使用，不知道wayland怎么样？
```
cd ~/projects/makepad
cargo run -p makepad-example-simple
```
然后就可以看到 running 了，不过一般来说 dock 那边没有出现图标……

结论是其他 robius 的 sample 在 Debian 下都没法跑，回到 sample 下进行工作吧！

### hello world

使用 simple 改装一下？