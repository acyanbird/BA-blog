---
title: "Debian 打包 2048游戏"
date: 2025-01-13T23:14:48+08:00
draft: true
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

ibncurses-dev debuild dpkg-buildpackage -b