---
id: 78
title: Ipcop-OpenVPN安装手记
date: 2007-10-18T10:29:35+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=134
permalink: '/2007-10-ipcop-openvpn%e5%ae%89%e8%a3%85%e6%89%8b%e8%ae%b0/'
bttc_cache:
  - 1273157082:0
  - 1273157082:0
categories:
  - 默认
---
Step 1、安装Ipcop  
下载Ipcop&nbsp; http://ipcop.org/  
安装就那样了，呵呵

Step 2、安装Zerina作为Openvpn  
下载 zerina http://www.zerina.de/  
把下载的搞到ipcop主机上，呵呵 ipcop没有wget和ftp，用scp吧，记得开启ssh哈  
怎么开启？我晕 http://ipcop:81/  
系统 -> ssh -> 知道该怎么做了吧。  
解压后 执行 # ./install

Step 3、配置Openvpn  
参照 <a href="http://www.zerina.de/zerina/?q=node/91" target="_blank">http://www.zerina.de/zerina/?q=node/91</a>

Step 4、我……