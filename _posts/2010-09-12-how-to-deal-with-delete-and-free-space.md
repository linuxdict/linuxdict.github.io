---
id: 589
title: How to deal with delete and free space
date: 2010-09-12T20:51:33+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=589
permalink: /2010-09-how-to-deal-with-delete-and-free-space/
categories:
  - Howto
tags:
  - tips
---
How to free/restore the space ?

When we tried to clean the disk space, maybe encounter this kind of issue. you rm some big files.
  
df -h doesn&#8217;t appear difference. but du -hs /directory seems different with df
  
simple answer maybe is : some process use the files. the process didn&#8217;t free it.

If you want to know details, here is the link:
  
http://www.cyberciti.biz/tips/freebsd-why-command-df-and-du-reports-different-output.html

>sudo lsof |grep ifs|grep deleted
  
java **17059** ifs **9**w REG 253,9 632315860 1212431 /apps/ifs/IFSV01/instance/IFSV01/logs/connectserver/ifsalert.0.log.1 (deleted)

>ls -la /proc/**17059**/fd/**9**
  
l-wx&#8212;&#8212; 1 ifs ifs 64 Sep 13 02:16 /proc/17059/fd/9 -> /apps/ifs/IFSV01/instance/IFSV01/logs/connectserver/ifsalert.0.log.1 (deleted)

Now how to restore it ?
  
>cp /proc/17059/fd/9 /apps/ifs/ifsalert.0.log.1.restored

Now how to free it ?
  
#> /proc/17059/fd/9

More explainations: http://www.unixwerk.eu/linux/deleted_files.html