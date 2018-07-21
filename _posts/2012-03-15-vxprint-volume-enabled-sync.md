---
id: 728
title: vxprint volume enabled sync
date: 2012-03-15T23:15:22+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=728
permalink: /2012-03-vxprint-volume-enabled-sync/
categories:
  - Linux_D
tags:
  - storage
---
v oravol &#8211; ENABLED SYNC 109297664 SELECT &#8211; fsgen
  
pl oravol-01 oravol ENABLED ACTIVE 109297664 CONCAT &#8211; RW
  
sd rootdisk01-09 oravol-01 rootdisk01 33554432 26214400 0 c2t1d0 ENA
  
sd rootdisk01-11 oravol-01 rootdisk01 60280832 83083264 26214400 c2t1d0 ENA
  
pl oravol-02 oravol ENABLED ACTIVE 109297664 CONCAT &#8211; RW
  
sd rootdisk02-10 oravol-02 rootdisk02 34066432 109297664 0 c3t0d0 ENA

ENABLED SYNC could happened when you do the vxassist and then ctrl+c incidently.

Solution:
  
vxvol -g rootdg -f resync oravol

this need wait a while.

no verbose progress shows up. you can check with following.
  
vxprint -g rootdg -l|grep -i sync
  
state: state=SYNC kernel=ENABLED cdsrecovery=2/2 (syncing)

Another tips:
  
df -h can&#8217;t find the change for vxresize. but vxprint shows up.
  
you can use fsadm -b to extend the fs.