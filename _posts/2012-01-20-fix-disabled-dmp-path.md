---
id: 709
title: Fix disabled dmp path
date: 2012-01-20T22:13:34+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=709
permalink: /2012-01-fix-disabled-dmp-path/
categories:
  - solaris
tags:
  - solaris
  - storage
---
root # /etc/vx/bin/vxdisksetup -i EMC0_146
  
VxVM vxdisksetup ERROR V-5-2-3628 The dmpnode EMC0_146 is disabled.Can not
  
proceed with vxdisksetup.

root # vxdisk list EMC0_146
  
Device: EMC0_146
  
devicetag: EMC0_146
  
type: auto
  
flags: online error private autoconfig
  
errno: Device path not valid
  
Multipathing information:
  
numpaths: 2
  
c5t5006048449AE7F48d149s2 state=disabled
  
c6t5006048C49AE7F77d149s2 state=disabled

<!--more-->


  
root # vxdisk path |grep EMC0_146
  
c5t5006048449AE7F48d138s2 EMC0_146 &#8211; &#8211; DISABLED
  
c6t5006048C49AE7F77d149s2 EMC0_146 &#8211; &#8211; DISABLED 

root # vxdmpadm enable path=c5t5006048449AE7F48d149s2
  
root # vxdisk path |grep EMC0_146
  
c5t5006048449AE7F48d149s2 EMC0_146 &#8211; &#8211; ENABLED
  
c6t5006048C49AE7F77d149s2 EMC0_146 &#8211; &#8211; DISABLED
  
root # vxdmpadm enable path=c6t5006048C49AE7F77d149s2
  
root # vxdisk path |grep EMC0_146
  
c5t5006048449AE7F48d149s2 EMC0_146 &#8211; &#8211; ENABLED
  
c6t5006048C49AE7F77d149s2 EMC0_146 &#8211; &#8211; ENABLED 

root # /etc/vx/bin/vxdisksetup -i EMC0_146
  
prtvtoc: /dev/vx/rdmp/EMC0_146: Unable to read Disk geometry errno = 0x6

\# we need label it first.
  
root # format -d c6t5006048C49AE7F77d149
  
Searching for disks&#8230;done
  
format> l
  
Ready to label disk, continue? y

format> s
  
Saving new disk and partition definitions
  
Enter file name[&#8220;./format.dat&#8221;]: 

format> q

root # /etc/vx/bin/vxdisksetup -i EMC0_146
  
root # vxdisk list EMC0_146
  
Device: EMC0_146
  
devicetag: EMC0_146
  
type: auto
  
hostid:
  
disk: name= id=1327117862.145.yourhost
  
group: name= id=
  
info: format=cdsdisk,privoffset=256,pubslice=2,privslice=2
  
flags: online ready private autoconfig autoimport
  
pubpaths: block=/dev/vx/dmp/EMC0\_146s2 char=/dev/vx/rdmp/EMC0\_146s2
  
version: 3.1
  
iosize: min=512 (bytes) max=2048 (blocks)
  
public: slice=2 offset=2304 len=70703616 disk_offset=0
  
private: slice=2 offset=256 len=2048 disk_offset=0
  
update: time=1327117863 seqno=0.1
  
ssb: actual_seqno=0.0
  
headers: 0 240
  
configs: count=1 len=1280
  
logs: count=1 len=192
  
Defined regions:
   
config priv 000048-000239[000192]: copy=01 offset=000000 disabled
   
config priv 000256-001343[001088]: copy=01 offset=000192 disabled
   
log priv 001344-001535[000192]: copy=01 offset=000000 disabled
   
lockrgn priv 001536-001679[000144]: part=00 offset=000000
  
Multipathing information:
  
numpaths: 2
  
c5t5006048449AE7F48d149s2 state=enabled
  
c6t5006048C49AE7F77d149s2 state=enabled