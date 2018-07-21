---
id: 718
title: 'Grub2: fix dual boot issue'
date: 2012-02-18T06:24:39+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=718
permalink: /2012-02-grub2-fix-dual-boot-issue/
categories:
  - linux
tags:
  - tips
  - Ubuntu
---
Trying boot from livecd to fix the dual boot issue.
  
ubuntu@ubuntu:~$ sudo grub-install /dev/sda
  
/usr/sbin/grub-probe: error: cannot find a device for /boot/grub (is /dev mounted?).

Solution:
  
set the /boot/grub path
  
root@ubuntu:~# mkdir /a; mount /dev/sda1 /a # sda1 is the root you installed linux
  
root@ubuntu:~# grub-install /dev/sda &#8211;boot-directory=/a/boot/grub
  
Installation finished. No error reported.