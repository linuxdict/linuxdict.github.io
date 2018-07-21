---
id: 612
title: readonly issue on disk
date: 2011-03-01T23:34:40+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=612
permalink: /2011-03-readonly-issue-on-disk/
categories:
  - linux
  - Linux杂记
tags:
  - tips
---
We have one server became readonly after update DMX.

Error logs:
  
Buffer I/O error on device dm-1, logical block 1545
  
lost page write due to I/O error on dm-1
  
ext3_abort called.
  
EXT3-fs error (device dm-1): ext3\_journal\_start_sb: Detected aborted journal
  
Remounting filesystem read-only
  
qla2xxx 0000:0d:00.0: scsi(0:0:0): Abort command issued &#8212; 1 11299f0 2002.
  
qla2xxx 0000:0d:00.1: scsi(1:0:0): Abort command issued &#8212; 1 113a04c 2002.
  
&#8230;&#8230;
  
qla2xxx 0000:0d:00.0: Unable to read SFP data (102/a0/0).
  
process \`sysctl&#8217; is using deprecated sysctl (syscall) net.ipv6.neigh.eth3.base\_reachable\_time; Use net.ipv6.neigh.eth3.base\_reachable\_time_ms instead.
  
ext3_abort called.
  
EXT3-fs error (device dm-1): ext3_remount: Abort forced by user
  
ext3_abort called.

mount -o remount,rw /apps
  
mount: block device /dev/mapper/xxxx is write-protected, mounting read-only

Solution: reboot the server, all fixed 🙁