---
id: 75
title: Nginx在FreeBsd下的安装与配置
date: 2007-10-12T15:46:30+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=137
permalink: '/2007-10-nginx%e5%9c%a8freebsd%e4%b8%8b%e7%9a%84%e5%ae%89%e8%a3%85%e4%b8%8e%e9%85%8d%e7%bd%ae/'
bttc_cache:
  - 1273157082:0
  - 1273157082:0
categories:
  - 默认
---
What for? Nginx is a great replacement of Apache with very low memory
  
footprint and contrary to Lighttpd, doesn&#8217;t suffer from memory leak
  
over time. You can then use all the memory left to unleash the power of
  
mysql for instance by increasing the default query cache.

真的有传说中的好吗？呵呵，试一下先。

Step1 安装必备软件   
&nbsp;&nbsp;&nbsp; MySQL+PHP+Pcre  
cd /usr/ports/database/mysql50-server && make install clean  
cd /usr/lang/php5/ && make install ……