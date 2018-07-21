---
id: 721
title: how to fix vxdisk/dmp state disabled
date: 2012-02-26T16:54:26+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=721
permalink: /2012-02-how-to-fix-vxdiskdmp-state-disabled/
categories:
  - Howto
  - solaris
tags:
  - Howto
  - storage
---
sometime you add new disk. will notice vxdisk list show path state=disabled.

vxdisk list c2t0d63s2
  
Multipathing information:
  
numpaths: 2
  
c2t0d63s2 state=disabled
  
c3t0d63s2 state=disabled

vxdmpadm enable path=c2t0d63s2
  
vxdmpadm enable path=c3t0d63s2

then it goes to
  
numpaths: 2
  
c2t0d63s2 state=enabled
  
c3t0d63s2 state=enabled