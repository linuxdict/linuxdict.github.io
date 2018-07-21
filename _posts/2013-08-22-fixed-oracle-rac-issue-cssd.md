---
id: 818
title: '(Fixed) Oracle RAC Issue &#8211; cssd'
date: 2013-08-22T22:30:41+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=818
permalink: /2013-08-fixed-oracle-rac-issue-cssd/
categories:
  - Linux_D
tags:
  - linux
  - oracle
---
Issue 1: cssd can&#8217;t start up during reboot. GC startup block cssd startup. disable GC auto start fixed the issue.

root@host_name# /ora/product/11.1.0.6a/bin/crsctl check crs
  
Failure 1 contacting Cluster Synchronization Services daemon
  
Cannot communicate with Cluster Ready Services
  
Cannot communicate with Event Manager

root@host_name# /ora/product/11.1.0.6a/bin/crsctl start crs
  
<!--more-->


  
root@host_name# /ora/product/11.1.0.6a/bin/crsctl check crs
  
Cluster Synchronization Services appears healthy
  
Cannot communicate with Cluster Ready Services
  
Cannot communicate with Event Manager

Issue 2: Disk group can&#8217;t be mounted.

SQL> alter diskgroup all mount;
  
alter diskgroup all mount
  
*
  
ERROR at line 1:
  
ORA-15032: not all alterations performed
  
ORA-15063: ASM discovered an insufficient number of disks for diskgroup
  
&#8220;MYDBT01&#8221;
  
ORA-15063: ASM discovered an insufficient number of disks for diskgroup
  
&#8220;MYDBBT01_ARC&#8221;

Notes from Oracle: most likely there is BCV/CLone, caused the disk not has correct Header info.

+ASMFMS:/apps/ora/home> kfed read /dev/vx/rdsk/ASMdg\_MYDB\_T01/MYDBT01-ora-archivelog01
  
KFED-00303: unable to open file &#8221;

root@host\_name# /ora/product/11.1.0.6a/bin/kfed read /dev/vx/rdsk/ASMdg\_MYDB_T01/MYDBT01-ora-archivelog01
  
kfbh.endian: 1 ; 0x000: 0x01
  
kfbh.hard: 130 ; 0x001: 0x82
  
kfbh.type: 1 ; 0x002: KFBTYP_DISKHEAD
  
kfbh.datfmt: 1 ; 0x003: 0x01
  
kfbh.block.blk: 0 ; 0x004: T=0 NUMB=0x0
  
kfbh.block.obj: 2147483648 ; 0x008: TYPE=0x8 NUMB=0x0

here is the situation:
  
root@host\_name# ls -l /dev/vx/rdsk/ASMdg\_MYDB_T01/MYDBT01-ora-archivelog01
  
crw&#8212;&#8212;- 1 root root 199, 65530 Aug 23 03:47 /dev/vx/rdsk/ASMdg\_MYDB\_T01/MYDBT01-ora-archivelog01
  
root@host\_name# chown oracle:dba /dev/vx/rdsk/ASMdg\_MYDB_T01/MYDBT01-ora-archivelog01
  
root@host\_name# ls -l /dev/vx/rdsk/ASMdg\_MYDB_T01/MYDBT01-ora-archivelog01
  
crw&#8212;&#8212;- 1 oracle dba 199, 65530 Aug 23 03:47 /dev/vx/rdsk/ASMdg\_MYDB\_T01/MYDBT01-ora-archivelog01

Got it ? we use VXVM to manage the ASM disk. VXVM normally import the DG with ROOT as owner.

so we can update chown command in /etc/rc.local, you need turn on DG auto import of course.

how to Set autoimport to VX DG ?
  
[root@beihdp01b ~]# vxdg -g appora set autoimport=no
  
[root@beihdp01b ~]# vxprint -l appora
  
Disk group: appora

Group: appora
  
info: dgid=1363578089.12.beihdp01a.bj.domain.com **noautoimport**
  
version: 180
  
alignment: 8192 (bytes)
  
activation: read-write
  
detach-policy: global
  
dg-fail-policy: dgdisable
  
ioship: off
  
copies: nconfig=default nlog=default
  
devices: max=32767 cur=4
  
minors: >= 27000
  
cds=on

[root@beihdp01b ~]# vxdg -g appora set autoimport=yes
  
[root@beihdp01b ~]# vxprint -l appora
  
Disk group: appora

Group: appora
  
**info: dgid=1363578089.12.beihdp01a.bj.domain.com**
  
version: 180
  
alignment: 8192 (bytes)
  
activation: read-write
  
detach-policy: global
  
dg-fail-policy: dgdisable
  
ioship: off
  
copies: nconfig=default nlog=default
  
devices: max=32767 cur=4
  
minors: >= 27000
  
cds=on