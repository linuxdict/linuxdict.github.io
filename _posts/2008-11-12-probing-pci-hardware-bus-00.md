---
id: 97
title: Probing PCI hardware (bus 00)
date: 2008-11-12T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=63
permalink: /2008-11-probing-pci-hardware-bus-00/
bttc_cache:
  - 1273356500:0
  - 1273356500:0
categories:
  - 默认
---
Linux安装时停止在Probing PCI hardware (bus 00)错误解决办法

环境：
  
主板是英特尔G35的芯片组。两G条子。硬盘：SATA接口。

操作系统 CentOS4.X

故障：
  
Linux安装时提示 Probing PCI hardware (bus 00)

原因：
  
与硬盘的接口及PCI接口有关。

解决办法：
  
启动到LINUX界面下按F3，后输入linux pci=nommconf 后回车即可。安装完后，重启时还需要输入。

安装完之后编辑 /etc/grub.conf 将pci=nommconf 附加到内核后面，在同一行上。如下所示：

<span style="font-weight:bold;">kernel /boot/vmlinuz-2.6.9-78.0.5.plus.c4smp ro root=LABEL=/ pci=nommconf</span>