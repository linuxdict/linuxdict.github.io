---
id: 484
title: How to Use Curl Control Home Router
date: 2010-01-08T17:52:43+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=484
permalink: /2010-01-how-to-use-curl-control-home-router/
bttc_cache:
  - 1273324671:0
  - 1273324671:0
categories:
  - Howto
---
If we need to check your router status, we can use curl to grep some information we need.

My Wireless Router: TP-Link

Command to check who is online:

$ curl &#8211;basic &#8211;user myuser:myPass http://myrouteip/userRpm/AssignedIpAddrListRpm.htm |grep &#8220;what we want&#8221;