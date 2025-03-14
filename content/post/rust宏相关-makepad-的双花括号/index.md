---
title: "Rust宏相关 Makepad 的双花括号"
date: 2025-02-18T11:33:40+08:00
draft: true
author: "acyanbird"
summary: "Rust宏相关 Makepad 的双花括号"
tags: ["rust", "makepad"]
---
以 [makepad book simple](https://github.com/acyanbird/makepad-book-simple) 为例子，我其实一直都不是很明白里面双花括号的作用

```
    // 定义 App 组件
    App = {{App}} {
        // 定义 UI 树的根节点
        ui: <Root>{
            // 定义主窗口
            main_window = <Window>{
                // 显示背景
                show_bg: true
                width: Fill,
                height: Fill
```
这个似乎就是只是定义一个 struct ，真正的 App 在下面会被定义上去……