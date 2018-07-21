---
id: 281
title: In the past time, I always used the CentOS
date: 2009-04-22T20:51:15+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=281
permalink: /2009-04-in-the-past-time-i-always-used-the-cent/
bttc_cache:
  - 1273351130:0
  - 1273351130:0
categories:
  - Linux_D
tags:
  - linux
---
In the past time, I always used the CentOS. but after I used OpenSUSE just about a week. I found that the OpenSUSE is more friendly than CentOS. 

I spent about 2 hours to settle lots of problems after I \`yum install bind\`
  
It don&#8217;t create named.conf and some need files. Faint !!

when I tried \`sudo /etc/init.d/named start\`
  
Locating /etc/named.conf failed: [FAILED]
  
what&#8217;s going on? I just
  
sudo cp /usr/share/doc/bind-9.3.4/sample/etc/named.conf /etc/
  
[edyliu@centos53-edy ~]$ sudo /etc/init.d/named startStarting named:
  
Error in named configuration:
  
/etc/named.conf:57: open: /etc/named.root.hints: file not found [FAILED]

Although I settled the problems after remove some samples and uneed things.
  
I still want to ask :
  
Why Can&#8217;t I start the service after It has been Installed successfully ?

But In OpenSUSE, it just works after the installation. 

What happened to you, My CentOS/RHEL ? Are you trying to go away from my focus ?

Data from http://distrowatch.com/

1 Ubuntu 2373>
  
2 openSUSE 1562< 3 Mint 1458< 4 Fedora 1372>
  
5 Debian 1221< 6 Mandriva 959= 7 PCLinuxOS 920< 8 Puppy 726= 9 MEPIS 689< 10 CentOS 687<