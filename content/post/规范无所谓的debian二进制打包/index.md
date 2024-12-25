---
title: "规范无所谓的debian二进制打包"
date: 2024-12-25T16:56:45+08:00
draft: false
author: "acyanbird"
summary: "如果有一个二进制，如何直接变成 deb 包呢？"
tags: ["打包"]
---

### 前情提要
#### 关于 /opt 目录
在Linux系统中，/opt目录是一个专门用于存放可选软件包的文件夹。/opt的名字来源于“optional”，表示该目录用于存放可选的软件包，将这些文件与核心文件分开。在/opt下安装的软件通常会将所有相关文件（如二进制文件、库文件和配置文件）集中在一个目录中，这使得管理和删除这些软件变得更加简单。例如，若要卸载某个应用程序，只需删除其对应的子目录即可。  
因此在我们安装二进制文件夹的时候选择安装在这个目录，删除的时候会方便点（喂）

### 需要的工具
我们这次使用了 `dh_make` 和 `debuild` ，请根据系统需求进行安装。

## 开始打包
首先我们创建需要的文件夹，因为只是尝试所以比较简单
```bash
test-0.0.1/
└── opt
    └── test
```

其中 test-0.0.1 是包名称（当然也有可能是域名），后面跟软件本身的版本号，当然发行版内部可能对于某个特定软件进行多次构建，但这个之后再说。这一次我们假定 opt 里的 test 是需要的二进制文件。可以在 opt 文件夹里创建：
```bash
cd opt
touch test
```
### 创建 debian 文件夹
之后进入 `test-0.0.1` 文件夹执行 `dh_make --createorig -s -n -y` 之后会生成一个 debian 目录，让我们看看里面有什么
```bash
debian/
├── changelog
├── control
├── copyright
├── manpage.1.ex
├── manpage.md.ex
├── manpage.sgml.ex
├── manpage.xml.ex
├── postinst.ex
├── postrm.ex
├── preinst.ex
├── prerm.ex
├── README
├── README.Debian
├── README.source
├── rules
├── salsa-ci.yml.ex
├── source
│   └── format
├── test.cron.d.ex
├── test.doc-base.ex
└── test-docs.docs
```
在有 ex 和 docs 后缀名的文件，以及 README 文件在这一次里并不需要，所以可以删除这些文件减小体积，在 `test-0.0.1` 文件夹下

```bash
rm debian/*.ex debian/*.EX
rm -rf debian/*.docs debian/README debian/README.*
echo "opt/ /" > ./debian/install
```
最后一行是在 debian 下创建 install 文件，意思是将 opt 文件夹，安装到执行 deb 文件电脑的根目录。这可以保证如果电脑里没有 opt 目录就会先创建目录，也不会动 opt 目录里的其他文件。  
目前最重要的是 control 文件，architecture 中的 any 会直接读取宿主机的架构，或者可以像 amd64 这样写死。
```
Source: test
Section: unknown
Priority: optional
Maintainer: acy <acy@unknown>
Rules-Requires-Root: no
Build-Depends:
 debhelper-compat (= 13),
Standards-Version: 4.6.2
Homepage: <insert the upstream URL, if relevant>
#Vcs-Browser: https://salsa.debian.org/debian/test
#Vcs-Git: https://salsa.debian.org/debian/test.git

Package: test
Architecture: any
Depends:
 ${shlibs:Depends},
 ${misc:Depends},
Description: <insert up to 60 chars description>
 <Insert long description, indented with spaces.>
 ```
### 创建 deb 文件
`debuild -b -us -uc -tc` 使用 debuild 创建 deb 文件，这会在 test-0.0.1 的同级生成文件 `test_0.0.1_amd64.deb` 
可以尝试进行安装
`sudo apt install ./test_0.0.1_amd64.deb`  
之后可以在 /opt 文件夹里面找到 test 文件 `ls /opt | grep test` 就能看到里面的 test 文件啦