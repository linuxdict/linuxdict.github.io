---
id: 90
title: mplayer/codec drvc.dll
date: 2008-11-02T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=76
permalink: /2008-11-mplayercodec-drvcdll/
bttc_cache:
  - 1273307941:0
  - 1273307941:0
categories:
  - Linux桌面
---
mplayer使用时出现下面错误

error：could not open required directshow codec drvc.dll

解决方法：

[root@localhost ~]# find /usr/lib -name drvc*
  
[root@localhost ~]# find /usr/lib -name drvc*
  
/usr/lib/codecs/drvc.so
  
[root@localhost ~]# ldd /usr/lib/codecs/drvc.so
  
linux-gate.so.1 => (0x00110000)
  
libstdc++.so.5 => <span style="color:Red;">not found</span>
  
libc.so.6 => /lib/libc.so.6 (0x00162000)
  
/lib/ld-linux.so.2 (0x004ed000)

sudo apt-get install libstdc++5