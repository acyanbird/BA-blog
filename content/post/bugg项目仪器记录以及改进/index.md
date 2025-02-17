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

主控 sensor 气温，风速，power supply 一个。本地模型，挑选跟声音不一样的部分再上传，把后端替换成更加精确解析的AI，能够额外分类。

降低成本，推广给观鸟人，收集更多有价值的数据。

由于我有观鸟经验，方便的开源信息收集是缺失的。服务能够拓展到其他国家，给这个发展出力。

可以把这篇文章提到的 AI 换成更加高级的AI（这个？），不过目前的可以在本地端跑，上传异常以及生物数据，开放给有需要的人标注。在线上服务器，结合其他的比如 birdnet（？）来进行更详细的输出。同时为了众包科学，可以开放这些有用的声音给感兴趣的人进行标注，提供更多信息。  

希望能够实现的是，能够24小时在线的 monitoring，但是不会所有的声音进行上传，通过pnas那篇文章使用的，进行噪音和物种分类的 AI 分析智能挑选声音上传，大部分声音应该是没什么用的，当然可以压缩存储起来。同时提供传感器接口，可以监测温度风速等其他数据。  
当然如果有实时监控需求也可以 fall back。  

查看一下树莓派车载电池能否运行更好的，好的mic更好的收音设备，前面是要进行硬件改良。 

在后端做对前端进行粗略打包的声音分析的AI，开放有意义的片段给大家打标记（particpatory science），用这个东西继续训练 AI。目前前端用的是 CNN，改进一下针对这个进行分类。  

### 改进方案
希望基于目前的方案进行改进，因为如果部署在野外传输的难度比较大，基于树莓派的过剩性能可以在本地端先跑一次上面提到的AI，首先剥离有用（比如噪音和生物活动声音）上传，剩下的可以本地压缩。之后在服务器端再用更好的AI方法实现进一步的分类，例如这是什么噪音和物种分类等。之后把生物叫声筛选出来之后，如果没有充足数据可以制作网站，让大家进行声音的标注区分，用来更好地训练模型！  
或者直接做 sound

声学收音 MB sonics ambisonics，要多加麦克风，高保真收集声音，声音的指向性。麦克风阵列（计算机算法），能耗（！）。voice activity detection! 当前是人声还是不是人声。Knowles V2S200D  

麦克风更换成 [DIGITAL VOICE VIBRATION SENSOR](https://www.mouser.kr/new/knowles/knowles-v2s200d-vibration-sensor/?srsltid=AfmBOooSEIcMSHdyFRiMxzyZ-H5t-RCfPZ6MWCfXuNqJub7qx5ovuU9v)   [下一个演示视频](https://www.youtube.com/watch?v=IdgiYgTGjPw)没有声孔，无惧防水！为了指向性问题。mems 麦克风。

### 需要更换
麦克风以及收音（测试什么声音更好），可以把 MEMS sound wave pass through the hole, so ther is Acoustic membrane prevent water come in, but also decrease sensitivity. or increase robustness.   
传感器接口，都是树莓派了，多搞点也没啥
电池！储能以及光伏设备！看起来必须是要使用太阳能  
查看树莓派性能是否可以改进


### 如何回答

1️⃣为什么申请这个项目  
我从初中开始喜欢  
2️⃣读完这个MSc项目后，打算干点儿啥  
中国观鸟市场的空白很大！如果可以的话希望ebird能够在境内使用，进行一些国内观鸟工具不足的补齐，或者对于康奈尔实验室提供的套件比如 ebird 什么的，进行本地化（去掉Google 服务，进行鸟种翻译什么的）。作为众包科学只有大家参与了才有足够的数据！所以我看到 bugg 之后觉得这是一个很有潜力的项目  
3️⃣最近看了什么research paper及追问  

4️⃣最近校外参加了哪些活动  
京东方的 嵌入式 Linux 驱动，deepin，基金公司以及 rust 开发。还有业余无线电  
5️⃣在MSc阶段，想着重做哪方面的研究  
我想要

### 传统生态
使用红外摄像机进行分析，要进行全类型监测不太可能，可能就是上鸟类了（）compell，3G 是没问题的。自己假设无线网络（？）自动数据采集器。太阳能电池。