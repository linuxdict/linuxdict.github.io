---
id: 711
title: 'VCS: fix dg disabled. cannot open &#8221; &#8221; for quotactl'
date: 2012-02-03T17:47:11+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=711
permalink: /2012-02-vcs-fix-dg-disabled-cannot-open-for-quotactl/
categories:
  - Howto
  - linux
tags:
  - vcs
---
root@myhost1# vxdisk list
  
DEVICE TYPE DISK GROUP STATUS
  
sdbu auto:cdsdisk emc1XXX DB_PRD online dgdisabled
  
sdbv auto:cdsdisk emc1XXX DBarc_PRD online dgdisabled

root@myhost1# vxdg deport DB_PRD
  
VxVM vxdg ERROR V-5-1-584 Disk group DB_PRD: Some volumes in the disk group are in use
  
<!--more-->


  
but df doesn&#8217;t show up anything related with DG.

/dev/vx/dsk/DB\_PRD/DBroot /BCV/DB vxfs noauto,\_netdev 0 0
  
/dev/vx/dsk/DB\_PRD/DB-ora /BCV/DB/ora vxfs noauto,\_netdev 0 0
  
/dev/vx/dsk/DBarc\_PRD/DB-ora-archivelog01 /BCV/DB/ora/archivelog01 vxfs noauto,\_netdev 0 0

root@myhost1# mount /BCV/DB
  
root@myhost1# mount /BCV/DB/ora
  
UX:vxfs mount.vxfs: ERROR: V-3-21300: cannot open &#8220;/BCV/DB/ora&#8221; for quotactl

root@myhost1#fuser -c /BCV/DB
  
Cannot stat file /proc/13919/fd/4: Input/output error
  
Cannot stat file /proc/13946/fd/5: Input/output error
  
root@myhost1#ps -ef|grep &#8220;13919|13946&#8221;
  
root 13919 1 0 Jan28 ? 00:00:00 bpbkar -r 1209600 -ru root -dt 0 -to 0 -clnt
  
root 13946 1 0 Jan28 ? 00:00:00 bpbkar -r 1209600 -ru root -dt 0 -to 0 -clnt
  
root@myhost1# kill -9 13919 13946

\# succeed deport the dg now.
  
root@myhost1# vxdg deport DB_PRD
  
root@myhost1# vxdg -C import DB_PRD
  
root@myhost1# vxdg list
  
NAME STATE ID
  
localnbu enabled,cds 1245484407.6.myhost1
  
DB_PRD enabled,cds 1286892006.172.myhost2