---
id: 808
title: syslog simple notes
date: 2013-08-14T18:39:00+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=808
permalink: /2013-08-syslog-simple-notes/
categories:
  - Howto
  - linux
  - solaris
tags:
  - tips
---
configure the syslog send to central log server

Reminder:
  
For historical reasons, the <Tab> key, not a simple blank space, is used to define white space between the selector on the left side of the line and the action on the right side. Throughout the Log Analysis configuration documents, we&#8217;ve used the <Tab> to remind you of this &#8212; but of course, when you look at the file, you&#8217;ll only see white space.

\# Solaris
  
*.debug;mail,lpr,news,uucp,local0,local1,local2**<tab>**@remote\_log\_server
  
\# Linux
  
\*.crit,auth.\*,mark.\*,user.notice,local3.\*,local5.\*,local6.\*,local7.\*,syslog.\*,authpriv.\*,daemon.\***<tab>**@remote\_log\_server

\# Bounce syslog
  
<!--more-->


  
#Test the setting
  
#Solaris
  
snoop udp port 514
  
#Linux
  
tcpdump port 514

\# open another tab issue following test.
  
logger -p auth.notice &#8220;Test&#8221;

Ref http://www.precision-guesswork.com/sage-guide/syslog-overview.html