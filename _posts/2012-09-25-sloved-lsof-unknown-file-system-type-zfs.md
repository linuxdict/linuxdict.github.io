---
id: 761
title: (Sloved) lsof, unknown file system type (zfs)
date: 2012-09-25T18:17:10+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=761
permalink: /2012-09-sloved-lsof-unknown-file-system-type-zfs/
categories:
  - Howto
  - solaris
tags:
  - solaris
---
Environment:
  
Solaris 10.
  
lsof version 4.77
  
root@solaris10:~# lsof |more
  
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
  
sched 0 root cwd unknown file system type (zfs), v_op: 0x60074 068940
  
init 1 root cwd unknown file system type (zfs), v_op: 0x60074 068940

Solution:
  
Install the latest lsof version
  
<!--more-->


  
wget ftp://lsof.itap.purdue.edu/pub/tools/unix/lsof/lsof_4.86.tar.bz2
  
gtar xf lsof_4.86.tar.bz2
  
cd lsof\_4.86\_src
  
./Configure solaris
  
or ./Configure solariscc
  
make
  
./lsof | more