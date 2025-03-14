---
title: "Lerobot 初始化"
date: 2025-03-13T14:06:05+08:00
draft: false
author: "acyanbird"
summary: "Lerobot 初始化"
tags: ["清华实习","具身"]
---

跑通这里给的 example，注意一下 clone 需要 [git-lfs](https://git-lfs.com/) 不然大文件无法下载，不知道 macos 和 window 是否有不同。

### 安装环境
安装之后记住默认安装路径，在默认 activate 上面选择 否 （不然每一次都会开启，会拖慢打开 Terminal 的速度）
`conda create -y -n lerobot python=3.10`
之后需要 `conda init` 来起始。把之前的 conda init 的代码块的注释掉

```bash
export PATH="/home/acy/miniconda3/bin:$PATH"
alias lr="source ~/miniconda3/bin/activate && conda activate lerobot"
```
把 miniconda 的可执行文件放在 path 变量下，之后使用alias，每次在 lerobot 的文件夹下就可以activate这个环境。然后如果要退出的时候连续输入 `conda deactivate`

进入到项目路径(比如 cd 到指定路径），然后安装依赖 `pip install -e ".[feetech]"`

如果是linux发行版
```bash
conda install -y -c conda-forge ffmpeg
pip uninstall -y opencv-python
conda install -y -c conda-forge "opencv>=4.10.0"
```

如果有遇到 ssl 认证问题，可以关闭 ssl 证书认证（虽然不安全但是work）
`conda install -y -c conda-forge "opencv>=4.10.0"`

### 寻找机械臂串口

首先按照[example](https://github.com/huggingface/lerobot/blob/main/examples/10_use_so100.md)的视频里面的做法，把usb和电源线接上。 `python lerobot/scripts/find_motors_bus_port.py` 跑一次找到这次是什么串口，Linux大概是是 `/dev/ttyACM0` 
可以通过 sudo chmod 666 /dev/ttyACM0 给予权限（如果权限不够的话。

修改串口的 config file，在 robot 的configs.py 里面 `lerobot/common/robot_devices/robots/configs.py`

```python
    leader_arms: dict[str, MotorsBusConfig] = field(
        default_factory=lambda: {
            "main": FeetechMotorsBusConfig(
                # port="/dev/tty.usbmodem58760431091", 这个大概是Windows的？
                port = "/dev/ttyACM0",
                motors={
```

### calibrate

这个应该是复位？一开始依赖库版本不对，额外安装 `conda install -c conda-forge jpeg libtiff`

## 总是出问题咱还是从组装开始吧

总结一下软件，无论用什么方法设置好 miniconda （以及不要让他每次都自动启动），安装依赖，如果不行关闭 ssl 验证，Debian 12 可能需要额外安装 `conda install -c conda-forge jpeg libtiff`  

