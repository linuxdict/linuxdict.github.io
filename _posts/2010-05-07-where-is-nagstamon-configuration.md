---
id: 558
title: Where is nagstamon configuration?
date: 2010-05-07T19:08:53+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=558
permalink: /2010-05-where-is-nagstamon-configuration/
bttc_cache:
  - 1273363922:0
  - 1273363922:0
categories:
  - Howto
tags:
  - monitor
  - nagios
  - tips
---
My nagstamon crashed sometimes and the configuration lost.

but can&#8217;t find where the hell configuration is. so got the solution: define the configuration manually.

> Everything should get at its place and you can start it from Start menu/Programs/nagstamon. When run from command line with &#8220;nagstamon&#8221; you can pass a configfile like &#8220;nagstamon configfile&#8221; in case you want to store it at another place than default. It starts automatically at login. Details: http://nagstamon.sourceforge.net/setup/

Now my shortcut looks like: &#8220;C:\Program Files\nagstamon\nagstamon.exe&#8221; nagconfig.conf
  
The configuration lays in C:\Program Files\nagstamon\nagconfig.conf , good news it also encryto the password. cool 🙂