---
id: 285
title: 'Tips: write a shell into /etc/crontab'
date: 2009-04-23T01:18:23+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=285
permalink: /2009-04-tips-write-a-shell-into-etccrontab-ch/
bttc_cache:
  - 1273205126:0
  - 1273205126:0
categories:
  - Linux_D
tags:
  - tips
---
Tips: write a shell into /etc/crontab check the service automatically

#!/bin/bash
  
PORT=:80 #The port, the : makes it easy to snag only ports and not other numbers in the output.
  
INITS=httpd #The name of the service in /etc/init.d/
  
COUNT=$(netstat -lpn | grep $ | wc -l)
  
if [ $COUNT -lt 1 ]
  
then
  
/etc/init.d/$INITS start
  
fi