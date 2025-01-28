---
title: "Bugg项目仪器记录以及改进"
date: 2025-01-27T21:59:50+08:00
draft: false
author: "acyanbird"
summary: "Bugg项目仪器记录以及改进"
# tags: [""]
---
目前来看他们是为了这个项目执行一个开源的解决方案，目前有三篇论文，最新的着力点在数据分析上面，使用声音辨识异常声响来报警。

[swift recorder](https://www.birds.cornell.edu/ccb/swift/) 43KHz 3周或者更多，3个 D cell battery（那是啥）

有了更简单的实现了，在 [IEEE](https://ieeexplore.ieee.org/document/10742275?utm_source=wiley&getft_integrator=wiley)

把这个和 raven 结合起来，然后直接做好接口给 ebird 进行 submit 不知道是否可行……

给观鸟人特供的recorder，夜晚收音以观测夜鸟版？

在此之前也有一个 [solo](https://solo-system.github.io/home.html) d £120 (including a 5-day battery, memory card and a really good microphone). The cost without battery and memory card is £83 (for comparison with commercial systems) 5天电池续航？

bugg 本身不提供供电选项，推荐亲亲购买额外电池或者太阳能板子（不要啊）（话说车载电池多少钱来着）

所以 bugg 系统总体续航未声明，单价80美刀这样？
### bugg参数


[开源声学网站集合](https://pmc.ncbi.nlm.nih.gov/articles/PMC7682500/) https://ecosound-web.de/ecosound_web/  

突破方向大概是可以deliver的低成本，并且有平台支持的处理？顺便可以在为标记地区比如中国使用？  

毕竟我之前写了希望开发观鸟工具，所以采取低成本的后院录音模块（可以对比一下康奈尔的照相喂鸟器？），用来采集叫声。然后通过拉通当地观鸟人，让他们帮助标记鸟叫来采集数据

[bird weather](https://app.birdweather.com/)  希望帮助构建的是这个！ 

先 focus on，低成本开源硬件的生态检测工具，有 live streaming 功能，可以自建后端或者使用其他的后端比如 birdweather，采集数据。可以接其他传感器记录温度，风速等气候数据

esp8266或8285 rp2040 通讯模组 RedCap模组 RG255AA