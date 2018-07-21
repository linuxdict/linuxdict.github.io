---
id: 605
title: client 4 rejected from IP x.x.x.x
date: 2010-12-25T17:29:23+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=605
permalink: /2010-12-client-4-rejected-from-ip-x-x-x-x/
categories:
  - Howto
tags:
  - tips
---
Xming.exe: client 4 rejected from IP 192.168.1.215

Solution:
  
Edit: X0.hosts (lay in the installation directory)
  
add the ip you want allow. my X0.hosts
  
&#8220;localhost
  
192.168.1.215&#8221;
  
Restart Xming.