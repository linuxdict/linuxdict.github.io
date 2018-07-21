---
id: 292
title: squidclient -p 3128 -h squid_ip_address
date: 2009-04-24T01:03:26+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=292
permalink: /2009-04-squidclient-p-3128-h-squid_ip_address/
bttc_cache:
  - 1273290411:0
  - 1273290411:0
categories:
  - Linux_D
tags:
  - squid
---
squidclient -p 3128 -h squid\_ip\_address mgr:info@PASSWORD 

get the squid manager infomation from it.
  
we should enable the client access cache manager
  
edit /etc/squid/{squid.conf, cachemgr.conf}
  
add your ip address to access. default manager can only access by localhost.

use a different port for cache manager
  
http\_port 80 defaultsite=want\_to\_access\_ip_address/hostname :80
  
http_port 8001 # this is for cache manager