---
id: 796
title: 'ssh_exchange_identification: Connection closed by remote host'
date: 2013-06-03T16:47:13+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=796
permalink: /2013-06-ssh_exchange_identification-connection-closed-by-remote-host/
categories:
  - linux
tags:
  - ssh
---
What&#8217;s wrong with the server ?

debug1: identity file /export/home/intprd/.ssh/id_dsa type 2
  
ssh\_exchange\_identification: Connection closed by remote host
  
Connection closed

if your sshd is busy, you may consider to increase the MaxStartups 10 -> MaxStartups 100, change the value according to your request.

more details you can get by turn debug on for sshd server LogLevel DEBUG

If you got error msg like following from messages/secure logs.
  
May 30 02:49:14 localhost sshd[19458]: [ID 800047 auth.debug] debug1: drop connection #10
  
May 30 02:49:15 localhost sshd[19458]: [ID 800047 auth.debug] debug1: drop connection #10 

which means you reach MaxStartups 10 now.