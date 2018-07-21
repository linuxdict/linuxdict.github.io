---
id: 725
title: oracle:dbca hang when click finish
date: 2012-03-14T05:52:49+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=725
permalink: /2012-03-oracledbca-hang-when-click-finish/
categories:
  - Howto
tags:
  - oracle
  - tips
---
this issue happen when you install Oracle with Creating DB. or use dbca to create DB.

Env, use Xming as X server. and foward Oracle X to Xming.
  
$export DISPLAY=192.168.1.103:0.0
  
$dbca
  
Warning: Cannot convert string &#8220;-b&h-lucida-medium-r-normal-sans-\*-140-\*-\*-p-\*-iso8859-1&#8221; to type FontStruct

Note, the Warning is the killer. which stopped dbca go foward

<!--more-->


  
You may check the trace log. every time you click the finish, it will show, FinishClicked: true
  
/app/oracle/product/10.2.0/db_1/cfgtoollogs/dbca/trace.log
  
\[AWT-EventQueue-0\] \[10:45:2:543\] [DBCAWizard.onFinish:1139] m_bFinishClicked: true

to fix it:
  
1. install the Xming-fonts which can be downloaded from Xming site.
  
2. use Linux computer as the X server.

Btw, you may met issue with X in linux.
  
X :0 -nolisten tcp
  
it doesn&#8217;t change even you updated the /etc/X11/xinit/xserverrc.
  
try this
  
add following lines to /etc/gdm/custom.conf

> [security]
  
> DisallowTCP=false

and reboot the computer. or restart gdm.