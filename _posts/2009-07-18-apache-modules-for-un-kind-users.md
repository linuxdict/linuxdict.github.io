---
id: 432
title: Apache modules for un-kind users
date: 2009-07-18T17:37:35+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=432
permalink: /2009-07-apache-modules-for-un-kind-users/
bttc_cache:
  - 1273344709:0
  - 1273344709:0
categories:
  - LAMP
---
Modules for block some un-kind users. to some extents, it can do some help with DDoS

Modules Name:
  
mod\_memcache\_block
  
FEATURES:
  
Distributed White and Black listing of IPs, ranges, and CIDR blocks
  
Configurable timeouts, memcache server listings
  
Support for continuous hasing using libmemcached’s Ketama
  
Windowded Rate limiting based on Response code (to block brute-force dictionary attacks against .htpasswd, for example)

http://github.com/netik/mod\_memcache\_block/tree/master

I wrote a shell scripts to trace Apache log formerly.
  
such as I read the last 50000 visit log, and check the same ip&#8217;s active status.
  
use iptables block it. and free it in some minutes laters.

this modules is more friendly i think.