---
title: "Rime输入法横排"
date: 2026-05-28T21:17:11+01:00
draft: false
author: "acyanbird"
summary: "Rime输入法横排"
# tags: [""]
---

更新之后本来的配置没了，这里说明一下。Linux的输入候选横排看这里

https://github.com/rime/ibus-rime/issues/42

修改 `~/.config/ibus/rime/build/ibus_rime.yaml` 文件，把里面的 horizontal: true 修改好，默认是false
```
__build_info:
  rime_version: 1.13.1
  timestamps:
    ibus_rime: 1735467225
    ibus_rime.custom: 0
config_version: 1.0
style:
  cursor_type: insert
  horizontal: true
  inline_preedit: true
  preedit_style: composition
```
贴一下整体的文件咪