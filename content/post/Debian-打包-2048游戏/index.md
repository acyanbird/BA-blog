---
title: "Debian 打包 2048游戏"
date: 2025-01-13T23:14:48+08:00
draft: false
author: "acyanbird"
summary: "Debian 打包 2048游戏"
# tags: [""]
---

放一下最新链接 [guide](https://www.debian.org/doc/manuals/debmake-doc/index.en.html)  
ummmm 看到 [proposal](https://www.debian.org/devel/wnpp/being_packaged) 这里有关于 [2048 游戏](https://github.com/alewmoose/2048-in-terminal)  

然后看到大概流程是这样

```
 $ tar -xzmf debhello-0.0.tar.gz
 $ cd debhello-0.0
 $ debmake
   ... manual customization
 $ debuild
   ...
```
首先要保证这个包最后包含版本号（不允许下划线），然后制作 tar.gz 包（反正是展开的的压缩包都需要有啦），之后进入目录执行 `debmake -x1`

 `debuild dpkg-buildpackage -b`
这是比较宽松的打包法则，不被Debian限制嗯……

 [前后的script](https://www.debian.org/doc/debian-policy/ch-maintainerscripts.html)
### 去提问的地方
在 [help resources](https://www.debian.org/doc/manuals/debmake-doc/ch03.en.html#help) 这里

### 查找依赖
生成了 deb 包之后，使用 `dpkg -f 2048-in-terminal_0.0-1_amd64.deb pre-depends depends recommends conflicts breaks` 这个命令查找，把 deb 换成对应的包名，在 control 的 depend 下更新一下

### 更新 Copyright
这个可以先不管……

好像 quilt 不知道怎么做？反正 install 是之前的，remove 应该也有 script postrm

### 移除软件
除了 install 之后要进行 postrm，在 remove 之前进行的，反正我叫 ChatGPT 生成一下~

```
#!/bin/sh
set -e

# Commands to run after the package is removed
echo "Running postrm script for 2048-in-terminal"
rm -f /usr/games/2048-in-terminal

exit 0
```