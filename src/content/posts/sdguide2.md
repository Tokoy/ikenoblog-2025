---
title: 'AI绘画工具webui简单入门 之 高清化'
published: 2023-03-19
description: '如何把生成的图高清化'
author: 'ike'
image: 'https://img.ikeno.top/202303223455651915.png'
tags: ["技术", "ACG", "AI", "绘图"]
category: blog
draft: false
---

**Webui直接生成出来的图会很模糊，而且有些地方细节不是很好，如果用作4k壁纸会感觉很别扭，所以需要高清修复。**
## 步骤
打开webui的图生图，调整参数为：  
* 缩放模式：`拉伸`  
* 采样方法(Sampler)：`DPM adaptive`  
* 宽度和高度在原有的基础上+64 ：`1280*720  --> 1344*784  `  
* 重绘幅度(Denoising)：`0.15`  
* 脚本：`使用SD放大（SD upscale）`  
* 放大算法：`R-ESRGAN 4x+ Anime6B`    
  
其他参数默认即可，最后点击生成等待成果吧！
## 放大前：
![放大前|inline](https://img.ikeno.top/20230322xskx4sold.png)

## 放大后：
![放大后|inline](https://img.ikeno.top/202303223455651915.png)

## 其他
最后再推荐一个网站，如果想要把生成的图做壁纸的话，可以把动漫图片用算法最大放大到2k甚至4K。  
**[waifu2x](https://waifu2x.udp.jp/)**
