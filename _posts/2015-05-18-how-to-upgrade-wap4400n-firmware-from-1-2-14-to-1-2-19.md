---
id: 883
title: How to upgrade WAP4400N firmware from 1.2.14 to 1.2.19
date: 2015-05-18T01:04:06+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=865
permalink: /2015-05-how-to-upgrade-wap4400n-firmware-from-1-2-14-to-1-2-19/
categories:
  - Howto
---
Seems it&#8217;s a old wireless Router. no new firmware released now.

Why I want to upgrade firmeware ? just for fun. didn&#8217;t feel much improvement. 🙂
  
Just got a official link
  
http://osdn.jp/projects/sfnet\_officiallinksysfirmware/downloads/wap4400n/1.2.19/WAP4400N\_GPL_v1.2.19.tar.bz2/

I had to use an GCC 3.x box. so I choose CentOS 4.8. so old.

Download firmware from above link, following the cross compile guide. will be straight forward.
  
Packages installed: gcc bison flex gcc-c++ zlib-devel
  
After a looong compile. got the new firemware 1.2.19.

Upgrade by your own risk 🙂

Get the firmware: http://192.168.1.77:8880/soft/wap4400n_v1219.img