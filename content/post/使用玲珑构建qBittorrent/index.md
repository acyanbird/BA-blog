---
title: "使用玲珑构建qBittorrent"
date: 2025-01-08T14:13:00+08:00
draft: false
author: "acyanbird"
summary: "使用玲珑构建qBittorrent"
# tags: [""]
---
玲珑是统信软件自研的开源软件包格式，用于替代 deb、rpm等包管理工具，实现了应用包管理、分发、容器、集成开发工具等功能。总之来用用看怎么打包！  
打包的前提是进行构建……首先构建一遍 sample project bittorrent 吧  

### 构建qBittorrent
首先在GitHub仓库拿到他的源代码，然后查看INSTALL文件
```
1) Install these dependencies:

  - Boost >= 1.76

  - libtorrent-rasterbar 1.2.19 - 1.2.x || 2.0.10 - 2.0.x
      * By Arvid Norberg, https://www.libtorrent.org/
      * Be careful: another library (the one used by rTorrent) uses a similar name

  - OpenSSL >= 3.0.2

  - Qt 6.5.0 - 6.x

  - zlib >= 1.2.11

  - CMake >= 3.16
      * Compile-time only

  - Python >= 3.9.0
      * Optional, run-time only
      * Used by the bundled search engine
```
可以通过 `dpkg -l | grep <包名>`检索一下是否安装（然后发现有一大堆没有安装）ummmm那先开始好了。先更新一下软件包罢……  
然后把 boost 装好就可以，我这里安装的是 libboost-all-dev 
首先安装 [libtorrent](https://github.com/arvidn/libtorrent) 
```
cmake -DCMAKE_BUILD_TYPE=Release\
-DCMAKE_INSTALL_PREFIX=$PREFIX ..
make -j$(nproc)
sudo make install
```
这样就安装好了 libtorrent。  
之后构建 qBittorrent，安装 libssl-dev, qt6-base-dev, qt6-svg-dev,qt6-tools-dev, libxkbcommon-dev, qt6-base-private-dev
