---
id: 894
title: when openssh will kick out idle users ?
date: 2016-05-31T21:05:35+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=894
permalink: /2016-05-when-openssh-will-kick-out-idle-users/
categories:
  - linux
tags:
  - ssh
---
when reading CIS security baseline. it mentions following lines: 

Having no timeout value associated with a connection could allow an unauthorized user access to another user&#8217;s ssh session (e.g. user walks away from their computer and doesn&#8217;t lock the screen). Setting a timeout value at least reduces the risk of this happening..
  
While the recommended setting is 300 seconds (5 minutes), set this timeout value based on site policy. The recommended setting for ClientAliveCountMax is 0. In this case, the client session will be terminated after 5 minutes of idle time and no keepalive messages will be sent.

Review our settings:
  
ClientAliveInterval 300
  
ClientAliveCountMax 1

According to man sshd_config
  
If ClientAliveInterval (see below) is set to 15, and ClientAliveCountMax is left at the default, unresponsive SSH clients will be disconnected after approximately 45 seconds. This option applies to protocol version 2 only.

Interesting thing is: you won&#8217;t be kicked out after 45s if you set as above with Protocol 2. 

From my test: the timeout will ONLY work when you set ClientAliveCountMax to 0. and idle time set to what you want kick out the user.