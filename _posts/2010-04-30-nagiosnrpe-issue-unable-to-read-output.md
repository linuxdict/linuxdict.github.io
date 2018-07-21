---
id: 546
title: 'Nagios/NRPE Issue: Unable to read output'
date: 2010-04-30T20:51:18+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=546
permalink: /2010-04-nagiosnrpe-issue-unable-to-read-output/
bttc_cache:
  - 1273363922:0
  - 1273363922:0
categories:
  - solaris
---
On Solaris you may met the following problem

&#8220;nagios &#8211; NRPE: Unable to read output&#8221;, may caused by the plugin, check the permission and libs

ldd /usr/local/nagios/libexec/check_disk , if it tell you &#8220;not found&#8221; , try to get the lib from www.sunfreeware.com

libintl.so.8 =>  /usr/local/lib/libintl.so.8
  
libiconv.so.2 =>         /usr/local/lib/libiconv.so.2
  
libsec.so.1 =>   /usr/lib/libsec.so.1
  
libc.so.1 =>     /usr/lib/libc.so.1
  
libpthread.so.1 =>       /usr/lib/libpthread.so.1
  
libdl.so.1 =>    /usr/lib/libdl.so.1
  
libgcc\_s.so.1 =>         /usr/local/lib/libgcc\_s.so.1
  
libavl.so.1 =>   /lib/libavl.so.1
  
libm.so.2 =>     /lib/libm.so.2

<!--more-->

#!/usr/bin/bash

groupadd nagios

useradd -G nagios nagios

for i in ALTnrpe-2.12-3-159-sol10-i386.pkg libgcc-3.4.6-sol10-x86-local libiconv-1.13.1-sol10-x86-local libintl-3.4.0-sol10-x86-local

do

pkgadd -d http://myhost/solaris/$i

done