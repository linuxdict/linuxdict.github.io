---
id: 555
title: 'Get the process like &#8220;netstat -anpt&#8221; on Solaris'
date: 2010-05-07T18:07:47+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=555
permalink: /2010-05-get-the-process-like-netstat-anpt-on-solaris/
bttc_cache:
  - 1273363922:0
categories:
  - Howto
tags:
  - solaris
  - tips
---
Two ways to get which process is Listen on the specific port on Solaris

1. lsof -i:port_number
  
e.g. lsof -i:22

2. Use scripts that combined with pfiles

e.g. get_port.sh 22

<!--more-->

#!/bin/bash

\# Get the process which listens on port

\# $1 is the port we are looking for

if [ $# -lt 1 ]

then

echo &#8220;Please provide a port number parameter for this script&#8221;

echo &#8220;e.g. $0 22&#8221;

exit

fi

echo &#8220;Greping for your port, please be patient (CTRL+C breaks) &#8230; &#8221;

for i in \`ls /proc\`

do

pfiles $i | grep AF_INET | grep $1 |grep -v pfiles

if [ $? -eq 0 ]

then

echo;echo &#8220;PID is $i and Process details run on port:$1&#8221;;echo

ps -cafe|grep $i|grep -v grep

fi

done