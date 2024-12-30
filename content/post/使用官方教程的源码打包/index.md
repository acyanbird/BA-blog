---
title: "使用官方教程的源码打包"
date: 2024-12-26T16:30:45+08:00
draft: false
author: "acyanbird"
summary: "使用官方教程的源码打包"
# tags: [""]
---

### 自定义 `debian/rules` 文件

在创建 Debian 包时，你可能需要自定义 `debian/rules` 文件。以下是一个示例 `debian/rules` 文件：

```makefile
#!/usr/bin/make -f

%:
    dh $@

override_dh_auto_configure:
    dh_auto_configure -- --with-kitchen-sink

override_dh_auto_build:
    make world
```

- `#!/usr/bin/make -f`：指定使用 `make` 作为解释器来执行这个文件。
- `%:`：通配符目标，表示所有目标。`dh $@` 将调用 `debhelper` 工具链中的适当命令来处理目标。
- `override_dh_auto_configure:`：覆盖目标，用于自定义 `dh_auto_configure` 的行为。
  - `dh_auto_configure -- --with-kitchen-sink`：传递 `--with-kitchen-sink` 选项给 `dh_auto_configure`，用于配置构建。
- `override_dh_auto_build:`：覆盖目标，用于自定义 `dh_auto_build` 的行为。
  - `make world`：调用 `make` 工具，并执行 `world` 目标来构建软件包。

通过这些步骤，你可以自定义 `debian/rules` 文件，以满足特定的构建需求。