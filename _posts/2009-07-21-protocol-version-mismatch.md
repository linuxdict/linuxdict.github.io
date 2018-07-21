---
id: 435
title: Protocol version mismatch
date: 2009-07-21T20:57:34+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=435
permalink: /2009-07-protocol-version-mismatch/
bttc_cache:
  - 1273344709:0
  - 1273344709:0
categories:
  - linux
tags:
  - backup
  - server
  - tips
---
I met the &#8220;aborted by signal=PIPE&#8221; when i used Backuppc to backup the remote server

so i run the commands on console:
  
>/usr/bin/ssh -q -x -l backup remote_ip /usr/bin/rsync &#8211;server &#8211;sender -v &#8211;ignore-times . /
  
protocol version mismatch &#8212; is your shell clean?
  
(see the rsync man page for an explanation)
  
rsync error: protocol incompatibility (code 2) at compat.c(171) [sender=3.0.4]

I search from internet, get the answer: &#8220;clean the .bashrc .bash_profile&#8221;&#8230;.
  
but still doesn&#8217;t work

Finally I got the answer, because the argLists was overwritten, so I changed backup. the Backuppc works.
  
the right argLists is :
  
/usr/bin/ssh -q -x -l backup remote_ip /usr/bin/rsync &#8211;server &#8211;sender &#8211;numeric-ids &#8211;perms &#8211;owner &#8211;group -D &#8211;links &#8211;hard-links &#8211;times &#8211;block-size=2048 &#8211;recursive &#8211;ignore-times . /