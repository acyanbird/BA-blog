---
title: "Deepin安装ibus Rime以及rime Ice"
date: 2025-01-08T15:07:35+08:00
draft: false
author: "acyanbird"
summary: "Deepin安装ibus Rime以及rime Ice"
# tags: [""]
---

用的最久的输入法！雾凇~虽然但是，并没有很深入地进行过设置，在 deepin 上没有被打包过（或许因为是已经有了内置的搜狗输入罢），但是还是很怀念，于是安装一下。

### 从源码编译
主流发行版都有打包好的，所以这次从源码编译看看——[下载源码](https://github.com/rime/ibus-rime)。直接 git clone：
```
Checkout the repository:

git clone https://github.com/rime/ibus-rime.git
cd ibus-rime

If you haven't installed dependencies (librime, rime-data), install those first:

git submodule update --init
(cd librime; make && sudo make install)
(cd plum; make && sudo make install)

Finally:

make
sudo make install
```
 —— 然后子模块初始化失败，单独 clone 之后进行安装，分别是 [librime](https://github.com/rime/librime/tree/7d9ad77fb5e8e6e330925de5e09c6ecfc2d2f4fd) 和 [plum](https://github.com/rime/plum/tree/ff888cbb9fce8c3f5b8b355baeb10685b2052b43) 后面那个是安装 recipe 的东西，进入目录执行 `make && sudo make install`

这俩都依赖 boost 啊…… 在这里是 boost-default
