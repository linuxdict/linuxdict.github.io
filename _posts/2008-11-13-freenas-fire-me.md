---
id: 100
title: Freenas Fire me !
date: 2008-11-13T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=66
permalink: /2008-11-freenas-fire-me/
bttc_cache:
  - 1273356500:0
  - 1273356500:0
categories:
  - 默认
---
不喜欢freenas了，不知道怎么回事。
  
今天捣鼓了好一会儿都没搞定
  
以前有些用户直接存到/etc/passwd 里面
  
今天建了一些存到了/var/etc/passwd里面
  
很奇怪，并且不给我创建目录。还要自己手动创建
  
还出现密码错误的现象。。。。。。。

我放弃了。让它搞崩溃了

freebsd 7的ssh需要加上这两行才能登录。
  
PermitRootLogin yes
  
PasswordAuthentication yes
  
要不然就出错。。。。。。
  
普通的用户不能 su ，确实够安全！
  
真的是“鱼和熊掌，不可兼得”