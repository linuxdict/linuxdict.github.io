---
id: 607
title: the optimization of ecshop
date: 2011-02-12T21:12:22+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=607
permalink: /2011-02-the-optimization-of-ecshop/
categories:
  - LAMP
tags:
  - LAMP
  - Php
---
One game with optimization of ecshop.

We use eaccelerator as op for php code. also tested APC and Xcache. seems EA is better on ecshop. it finally turn out the speed is slow down by the session on DB part.

ecshop stores the session into DB. so there are lots of insert/update when the visit cocurrency is very high. but the DB load looks normal, that&#8217;s why we spent some time to hit the point. finally check with show processlist. found lots of operation on session table.
  
then we commented the code related with session. the speed of the site improved a lot. 

session be stored in DB maybe better with security or load banlance. but it can be replaced with Memcache. the speed should improve a lot.

Tips from on LAMP op:
  
http://www.ibm.com/developerworks/linux/library/os-5waystunelamp/index.html