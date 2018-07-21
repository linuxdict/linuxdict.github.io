---
id: 858
title: 'Howto: Restore VG with LVM backup.'
date: 2015-03-02T23:40:09+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=858
permalink: /2015-03-howto-restore-vg-with-lvm-backup/
categories:
  - Howto
tags:
  - linux
  - lvm
---
Like cbr in VxVM, LVM has also backup in /etc/lvm/archive/, so if you accidentally remove VG, or VG got destroyed. you can try following procedure. 

Note: better do disk2disk copy before doing following. No grantee for your data. 

[root@mytesthost:~]# cd /etc/lvm/archive/

[root@mytesthost:/etc/lvm/archive]# ls -lart .
  
total 36
  
-rw&#8212;&#8212;- 1 root root 919 Oct 22 13:34 VG-data_00000-1897227548.vg
  
-rw&#8212;&#8212;- 1 root root 923 Oct 22 13:51 VG-data_00001-659586034.vg
  
<!--more-->

-rw&#8212;&#8212;- 1 root root 1365 Oct 23 11:00 VG-data_00002-387427799.vg
  
-rw&#8212;&#8212;- 1 root root 922 Oct 23 11:00 VG-data_00003-963150977.vg
  
-rw&#8212;&#8212;- 1 root root 1360 Oct 23 11:27 VG-data_00004-1064511230.vg
  
-rw&#8212;&#8212;- 1 root root 1782 Oct 23 12:53 VG-data_00005-1898800676.vg
  
drwxr-xr-x. 6 root root 4096 Jan 29 10:00 ..
  
-rw&#8212;&#8212;- 1 root root 2189 Feb 26 09:44 VG-data_00006-1747892781.vg
  
drwx&#8212;&#8212;. 2 root root 4096 Feb 26 09:44 .

[root@mytesthost:/etc/lvm/archive]# sudo vgcfgrestore -f /etc/lvm/archive/VG-data_00006-1747892781.vg &#8211;verbose VG-data
      
DEGRADED MODE. Incomplete RAID LVs will be processed.
    
Restored volume group VG-data
  
[root@mytesthost:/etc/lvm/archive]# lvdisplay
    
&#8212; Logical volume &#8212;
    
LV Path /dev/VG-data/hdfs
    
LV Name hdfs
    
VG Name VG-data
    
LV UUID qbgsQq-yOOh-fHyt-XXXq-hFpU-2vfH-h6xGPb
    
LV Write Access read/write
    
LV Creation host, time mytesthost.rm.symbiosys.com.cn, 2014-10-23 11:00:49 +0800
    
LV Status NOT available
    
LV Size 50.00 GiB
    
Current LE 12800
    
Segments 1
    
Allocation inherit
    
Read ahead sectors auto

&#8212; Logical volume &#8212;
    
LV Path /dev/VG-data/solr
    
LV Name solr
    
VG Name VG-data
    
LV UUID r2qSiu-vJHT-LCXZ-QyyS-J2Py-ywyv-79ivsk
    
LV Write Access read/write
    
LV Creation host, time mytesthost.rm.symbiosys.com.cn, 2014-10-23 11:27:46 +0800
    
LV Status NOT available
    
LV Size 10.00 GiB
    
Current LE 2560
    
Segments 1
    
Allocation inherit
    
Read ahead sectors auto

&#8212; Logical volume &#8212;
    
LV Path /dev/VG-data/mongodb
    
LV Name mongodb
    
VG Name VG-data
    
LV UUID z1w1dY-lM63-EfjU-W21o-cAr6-keGd-j3lqYy
    
LV Write Access read/write
    
LV Creation host, time mytesthost.rm.symbiosys.com.cn, 2014-10-23 12:53:15 +0800
    
LV Status NOT available
    
LV Size 20.00 GiB
    
Current LE 5120
    
Segments 1
    
Allocation inherit
    
Read ahead sectors auto

[root@mytesthost:/etc/lvm/archive]# vgs
    
VG #PV #LV #SN Attr VSize VFree
    
VG-data 1 3 0 wz&#8211;n- 100.00g 20.00g
  
[root@mytesthost:/etc/lvm/archive]# df -h
  
Filesystem Size Used Avail Use% Mounted on
  
/dev/xvda1 20G 3.8G 15G 20% /
  
tmpfs 3.9G 0 3.9G 0% /dev/shm
  
[root@mytesthost:/etc/lvm/archive]# vgchange -ay /dev/VG-data
    
3 logical volume(s) in volume group &#8220;VG-data&#8221; now active
  
[root@mytesthost:/etc/lvm/archive]# mount /var/lib/mongodb/
  
[root@mytesthost:/etc/lvm/archive]# df -h
  
Filesystem Size Used Avail Use% Mounted on
  
/dev/xvda1 20G 3.8G 15G 20% /
  
tmpfs 3.9G 0 3.9G 0% /dev/shm
  
/dev/mapper/VG&#8211;data-mongodb
                         
20G 9.0G 9.7G 48% /var/lib/mongodb
  
[root@mytesthost:/etc/lvm/archive]#