---
id: 449
title: Home permission
date: 2009-08-12T23:48:22+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=449
permalink: /2009-08-home-permission/
bttc_cache:
  - 1273284807:0
  - 1273284807:0
categories:
  - LAMP
tags:
  - apache
  - linux
---
when we open user_dir in apache, we should change the /home as 711
  
i changed it to 711 no,but still have some problems

the developer use Ruby , it shows the following in apache error log.
  
Permission denied: xsendfile: cannot open file:
  
change the directory that store the file, it works well.

so seldom use /home/user to store some files that apache will visit.