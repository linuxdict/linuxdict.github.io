---
id: 730
title: 'Some tips: Vsftpd configuration'
date: 2012-04-05T18:11:46+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=730
permalink: /2012-04-some-tips-vsftpd-configuration/
categories:
  - Howto
  - Linux_D
tags:
  - ftp
  - tips
---
Vsftpd tips:

All following update /etc/vsftpd/vsftpd.conf

How to change the default public root ?
  
anon_root=/the/path/you/want

I don&#8217;t want let my firewall too open. then define the min/max port.
  
pasv\_min\_port=60000
  
pasv\_max\_port=65000

iptable setting. 20 is for data
  
\# for FTP
  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 20 -j ACCEPT
  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 21 -j ACCEPT
  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 60000:65000 -j ACCEPT

Vsftp default turn Passive on, How to disable it ?
  
pasv_enable=NO