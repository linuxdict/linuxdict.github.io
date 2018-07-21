---
id: 89
title: Apache的Alias
date: 2008-10-20T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=69
permalink: '/2008-10-apache%e7%9a%84alias/'
bttc_cache:
  - 1273337363:0
  - 1273337363:0
categories:
  - LAMP
---
昨天给朋友共享一个电影，没有QQ，MSN又太慢。
  
还是用我的Apache吧，因为我的电影在Windows的盘里，
  
挂载上之后做别名，就是403错误，看日志吧。
  
Alias /movie/ /media/disk/video/
  
&#8216;<&#8216;Directory &#8220;media/disk/video/&#8221; &#8216;>&#8217;
  
Options Indexes
  
Order allow,deny
  
Allow from all
  
&#8216;<&#8216;/Directory&#8217;>&#8217;
  
注:因为它害怕恶意代码，所以你要把单引号去

<!--more-->

日志只是提示refused by server
  
应该是权限问题
  
edyliu@edyliu-laptop:~$ ll /media/disk/video/
  
总用量 11556160
  
drwx&#8212;&#8212; 3 edyliu root 32768 2008-11-14 09:18 .
  
drwx&#8212;&#8212; 16 edyliu root 32768 1970-01-01 08:00 ..
  
-rwx&#8212;&#8212; 1 edyliu root 394587728 2007-10-17 03:07 01.rmvb

果然是 直接把 apache的用户改了
  
User edyliu
  
Group edyliu

$sudo service httpd graceful

访问OK!
  
记住：manual
  
因为我的电影是中文名，所以直接indexes出现乱码问题，
  
所以在httpd-autoindex.conf里面修改
  
`IndexOptions Charset=UTF-8`