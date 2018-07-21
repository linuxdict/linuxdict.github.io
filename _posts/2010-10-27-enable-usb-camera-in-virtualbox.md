---
id: 598
title: Enable USB Camera in Virtualbox
date: 2010-10-27T04:43:10+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=598
permalink: /2010-10-enable-usb-camera-in-virtualbox/
categories:
  - Howto
  - linux
tags:
  - tips
  - virtualbox
---
Due to some IM need camera in my virtualbox. get the result from ubuntu
  
 ``if [ "`grep vboxusers /etc/group|grep $USER`" == "" ] ; then sudo usermod -G vboxusers -a $USER ; fi`` 
  
restart the virtualbox. and follow the following instructions
  
DO NOT add the line to /etc/fstab, or you may meet some issue 🙂
  
`none /proc/bus/usb usbfs devgid=groupid,devmode=664 0 0`
  
Details
  
https://help.ubuntu.com/community/VirtualBox/USB

Also: furiusisomount can mount .bin file that can be mount as cd-rom in Windows.