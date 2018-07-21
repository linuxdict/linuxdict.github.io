---
id: 284
title: 'Q: when you umount /mnt/usb it shows: um&#8230;'
date: 2009-04-22T23:25:19+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=284
permalink: /2009-04-q-when-you-umount-mntusb-it-shows-um/
bttc_cache:
  - 1273280779:0
  - 1273280779:0
categories:
  - Linux_D
tags:
  - tips
---
Q: when you umount /mnt/usb it shows:
  
umount: /mnt/usb: device is busy
  
umount: /mnt/usb: device is busy

A: > lsof +D /mnt/usb
  
find the PID of using /mnt/usb, kill it or quit the application.