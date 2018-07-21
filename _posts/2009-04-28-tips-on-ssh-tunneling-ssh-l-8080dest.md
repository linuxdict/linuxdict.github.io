---
id: 301
title: tips on ssh tunneling
date: 2009-04-28T20:40:30+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=301
permalink: /2009-04-tips-on-ssh-tunneling-ssh-l-8080dest/
bttc_cache:
  - 1273307853:0
  - 1273307853:0
categories:
  - Linux_D
tags:
  - tips
---
tips on ssh tunneling 

ssh -L 8080:destination\_ip/dns:80 local\_net/other

now you can visit the destination_ip/dns by visit

localhost:8080

more details:
  
http://www.securityfocus.com/infocus/1816/
  
http://en.wikipedia.org/wiki/Tunneling_protocol
  
http://www.revsys.com/writings/quicktips/ssh-tunnel.html
  
http://www.engadget.com/2006/03/21/how-to-ssh-tunnels-for-secure-network-access/