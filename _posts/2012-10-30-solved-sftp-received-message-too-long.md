---
id: 768
title: '(Solved) sftp: Received message too long'
date: 2012-10-30T19:00:38+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=768
permalink: /2012-10-solved-sftp-received-message-too-long/
categories:
  - Howto
  - linux
  - solaris
tags:
  - tips
---
when you connect by ssh. it works fine. but doesn&#8217;t work with sftp ?

check your ~user/.bashrc or ~user/.profile or ~user/.cshrc anything related with your environment.

remove the echo from above files.

addons: check free memory on Solaris without top
  
`vmstat 1 2 | tail -1 | awk '{printf "%d%s\n", ($5*4)/1024, "MB" }'`