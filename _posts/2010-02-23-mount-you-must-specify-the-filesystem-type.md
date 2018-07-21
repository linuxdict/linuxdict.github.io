---
id: 496
title: 'mount: you must specify the filesystem type'
date: 2010-02-23T04:01:41+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/2010-02-mount-you-must-specify-the-filesystem-type/
permalink: /2010-02-mount-you-must-specify-the-filesystem-type/
bttc_cache:
  - 1273362105:0
  - 1273362105:0
categories:
  - Linux_D
---
I have one raw file contains system:
  
$file my.raw
  
my.raw: x86 boot sector; partition 1: ID=0x83, active, starthead 1, startsector 63, 64259937 sectors; partition 2: ID=0x5, starthead 254, startsector 64260000, 2843505 sectors
  
try
  
$mount -o loop my.raw /mnt
  
mount: you must specify the filesystem type

Solution:
  
$mount -o loop,offset=32256 my.raw /mnt

Root:
  
The number too big for calculations, so set offset here.