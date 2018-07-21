---
id: 323
title: Install my wireless card driver
date: 2009-05-16T00:48:43+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=323
permalink: /2009-05-i-have-just-install-my-wireless-card-dri/
bttc_cache:
  - 1273323299:0
  - 1273323299:0
categories:
  - Linux桌面
tags:
  - linux
  - personal
  - tips
---
I have just install my wireless card driver ( bcm4312) on opensuse 11.1 (64bit)
  
my laptop is dell 1310

I use the most simple way
  
sudo zypper ar http://packman.mirrors.skynet.be/pub/packman/suse/11.1/ pack_man
  
sudo zypper install broadcom-wl
  
sudo reboot
  
the wireless card works.

install flash player x86_64 for firefox
  
http://labs.adobe.com/downloads/flashplayer10.html
  
sudo mkdir /usr/lib64/firefox/plugins
  
sudo cp libflashplayer.so /usr/lib64/firefox/plugins/

ref links
  
http://en.opensuse.org/HCL/Network\_Adapters\_(Wireless)/Broadcom_BCM43xx