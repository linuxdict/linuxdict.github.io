---
id: 625
title: 'Solaris: get global zone name from non-global zone'
date: 2011-05-23T17:39:31+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=625
permalink: /2011-05-solaris-get-global-zone-name-from-non-global-zone/
categories:
  - solaris
tags:
  - solaris
  - tips
---
run the netstat -p from non-global zone, get the ip information.
  
check the ip. one of the ip should be global zone&#8217;s ip. 

there is any commands to check ? No.
  
so we&#8217;d better keep a good record, like motd. or cmdb.