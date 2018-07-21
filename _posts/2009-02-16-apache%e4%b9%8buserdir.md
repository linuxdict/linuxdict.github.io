---
id: 203
title: Apache之userdir
date: 2009-02-16T15:07:38+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=203
permalink: '/2009-02-apache%e4%b9%8buserdir/'
bttc_cache:
  - 1273340352:0
  - 1273340352:0
categories:
  - LAMP
---
Apache有个userdir的模块
  
http://httpd.apache.org/docs/2.2/howto/public_html.html

以前没用过，想用一下，可是就是很403，日志也是简单的
  
Permission denied: access to /~username denied

后来在另一台用yum安装的服务器上找到答案。
  
\# The path to the end user account &#8216;public_html&#8217; directory must be
  
\# accessible to the webserver userid. This usually means that ~userid
  
\# must have permissions of 711, ~userid/public_html must have permissions
  
\# of 755, and documents contained therein must be world-readable.
  
\# Otherwise, the client will only receive a &#8220;403 Forbidden&#8221; message.

具体操作过程就是　
  
#chmod -R 711 /home/*
  
#cd /home/username/
  
#chmod 755 -R public_html

一切正常了。