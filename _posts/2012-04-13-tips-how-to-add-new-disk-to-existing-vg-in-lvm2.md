---
id: 734
title: 'Tips: how to add new disk to existing VG in Lvm2'
date: 2012-04-13T19:33:15+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=734
permalink: /2012-04-tips-how-to-add-new-disk-to-existing-vg-in-lvm2/
categories:
  - Howto
tags:
  - lvm
  - tips
---
We added new Hard disk. need add it to existing DG

take sdb as newly added disk

Step1: Format new disk and label as LVM disk
  
fdisk /dev/sdb
  
n -> p -> 1 -> return twice -> t -> 8e -> w

Step2: Create FS on new disk
  
mkfs.ext3 /dev/sdb1

Step3: Create as PV
  
pvcreate /dev/sdb1
  
<!--more-->

Step4: Extend existing VG to new disk
  
vgextend VolGroup00 /dev/sdb1
  
then, you will get more free space now. check with:
  
vgs 

Step5: Extend the Vol
  
lvextend -L +total\_space\_for\_vol\_g /dev/VolGroup00/LogVol00
  
lvextend -L +space\_number\_to\_add\_g /dev/VolGroup00/LogVol00

Step6: Online resize the Vol
  
resize2fs /dev/VolGroup00/LogVol00

Step7: Done.