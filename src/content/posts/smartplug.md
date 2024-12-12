---

title: '用Siri来控制Windows电脑开机关机吧'
published: 2024-02-26
description: '用siri来控制windows电脑开机和关机'
author: 'ike'
image: 'https://p1.itc.cn/q_70/images03/20230703/451f19066bc94b5cbdf88f5380b2310f.jpeg'
tags: ["技术", "日常", "智能插座","siri","PC","Windows"]
theme: 'light'
featured: false
---

## 前因
自从手机从iphone换成Android后，咱的13香就没啥用了，只能放桌子上当时钟，感觉有点浪费啊，所以研究了下苹果的HomeKit，用旧手机当智能中控岂不更好！网上查了下，貌似也蛮简单的。开搞开搞！

## 准备
1. 买一个能够连接homekit的智能插座，网上蛮多的，一个插座也就20~50不等，我买的是meross的，好像说是外贸货，反正到手是日本那边的，还行。买来后插上电，用手机先连接2.4g的wifi后扫描下二维码后按提示就可以让插座联网了，加入后只要网络正常，就可以用手机控制插座开关了。  
2. 设置电脑bios，通电后自动启动机器。我的外星人台式机是开机后按F2就可以进入bios，然后找到高级选项--电源选项里有个开机改成通电就Power On就好了。  
3. 给Windows账号加上密码，就是登陆要输入密码才能登陆，这样可以让其他手机或者服务器进行ssh登陆。  
4. 电脑安装OpenSSH。打开Powershell，然后``Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0``命令，出现进度条后等待安装完毕。然后net start sshd即可启动ssh服务。当然别忘了在防火墙的入站规则里加上TCP的22端口规则允许。还有就是在Windows的服务里找到OpenSSH然后手动改成自动，这样就开机自动启动啦。然后还有就是要把电脑的IP改成静态的，不能DHCP动态分配。最后可以尝试在Powershell里``ssh 你的用户名@你的服务器IP``，然后输入你的密码就可以正常SSH登陆啦！  

## 嘿 Siri
1. 准备工作都弄完后，现在就轮到iphone了，先在家庭里创建2个场景，一个是关电脑，就是控制插座关闭电源，另一个的开电脑，控制插座开启电源。弄完后点击试试，看看插座是不是可以正常点一下就开启和关闭了。  
2. 打开苹果的快捷指令，创建一个新的快捷指令，名称叫``打开电脑``,里面只需要添加``开电脑``的场景即可。这样只需要喊"嘿！sir，打开电脑" ，就可以开启插座然后通电开机啦。  
3. 再创建一个新的快捷指令，名称叫``关闭电脑``,然后添加``通过SSH发送命令``,把服务器的ip、22端口号、用户名、密码都填写，脚本的话填写``shutdown -s -t 1``。然后再添加等待60秒，最后再添加``关电脑``的场景即可。这样通过siri喊"嘿！sir，关闭电脑"，就可以实现快速关机了！ 

## 语音控制
上面通过嘿siri来控制快捷指令来运行关机貌似会有点小问题，因为要等待60s后才会执行下一步，siri好像默认不会等那么久，所以换一种方式，用iphone的``辅助功能``。里面有个语音控制，开启后新增语音``关闭电脑``然后运行对应的快捷指令即可，这下连siri都不用了，直接说关闭电脑就好了！ 

## 控制中台
iphone的家庭里其实还有一个小功能，就是开启引导界面，然后输入密码设置，你会发现界面会钉在家庭的控制页面，且不会切换，这样就相当于把手机作为了中台，只需要连接电源然后挂在墙上或者桌子上，就可以当一个完美的控制中台啦~  

## 最后
家里马上也要开始装修弄家具了，之前也有了解一些智能家居，但感觉都不是很实用，大部分也就是一些回家后自动开灯，开电器。起床自动打开窗帘和播放音乐之类的，为了这些多花好几万感觉不是很划算，那还不如就简单点用智能插座加场景设置和快捷指令来控制，这样成本低，自己diy，体验也不错。虽然有一些局限性，但本来就图新鲜，好玩就行了~  