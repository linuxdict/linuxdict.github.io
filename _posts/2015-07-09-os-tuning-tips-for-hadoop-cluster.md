---
id: 886
title: OS Tuning tips for Hadoop Cluster
date: 2015-07-09T18:36:17+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=872
permalink: /2015-07-os-tuning-tips-for-hadoop-cluster/
categories:
  - Howto
tags:
  - hadoop
---
1.Decrease swappiness.
  
Reason:
  
A value from 0 to 100 which controls the degree to which the system swaps. A high value prioritizes system performance, aggressively swapping processes out of physical memory when they are not active. A low value prioritizes interactivity and avoids swapping processes out of physical memory for as long as possible, which decreases response latency. The default value is 60.

Default value: 60
  
Recommend value: 5
  
Online Change: Y
  
Action:
  
\# update online
  
echo 5 > /proc/sys/vm/swappiness

\# update permanently , edit /etc/sysctl.conf and add following line:
  
vm.swappiness = 5
  
<!--more-->

2.Filesystem remount with noatime
  
Reason:
  
Ext4 default mount with atime, means the IO will update the filesystem with access time. Will bring extral IO to disk, atime useless to your HDFS filesystem, while noatime, means write operation will not update inode access times on this file system.
  
Default value: atime
  
Recommend value: noatime
  
Online Change: Y
  
Action:
  
\# update online
  
mount -o remount,noatime /dataX
  
\# update permanently , edit /etc/fstab
  
/dev/sdxx /dataX ext4 defaults,noatime 1 1

3.Turn off reserved disk for HDFS disks
  
Reason:
  
As a security measure the ext3 file system reserves 5% of device space for administrative processes. This protects the system by allowing root processes to continue using the disk if a user process runs wild and fills it up. With today’s larger disk capacities, 5% equates into gigabytes of arguably wasted space. This is unnecessary for HDFS because it has 3 replica. It’s safe to disable it.Based on our current disks. 0.2Tx30x6 = 36T. We are wasting 36T space.
  
Default value: 5%
  
Recommend value: 0%
  
Online Change: Y
  
Action:
  
\# this online change, no impact. Note: only do following on HDFS data disks.
  
sudo tune2fs -m 0 /dev/sdcX
  
tune2fs 1.41.12 (17-May-2010)
  
Setting reserved blocks percentage to 0% (0 blocks)
  
4.Disable transparent hugepage(THP) compaction
  
Reason:
  
Most Linux platforms supported by CDH 5 include a feature called transparent hugepage compaction which interacts poorly with Hadoop workloads and can seriously degrade performance.
  
Default value: enabled
  
Recommend value: disable
  
Online Change: Y
  
Action:
  
\# online update
  
echo never > /sys/kernel/mm/transparent_hugepage/enabled
  
echo never > /sys/kernel/mm/redhat\_transparent\_hugepage/defrag
  
\# update permanently , add following lines to /etc/rc.local
  
echo never > /sys/kernel/mm/redhat\_transparent\_hugepage/enabled
  
echo never > /sys/kernel/mm/redhat\_transparent\_hugepage/defrag

5.Vitual Memory tuning.
  
Reason:
  
OS default use overcommit ratio to 50%, means we have some waste of our RAM.
  
Default value: 50
  
Recommend value: 95
  
Online Change: Y
  
Action:
  
\# online update
  
echo 95 > /proc/sys/vm/overcommit_ratio
  
echo 2 > /proc/sys/vm/overcommit_memory
  
\# update permanently , add following lines to /etc/sysctl.conf
  
vm.overcommit_ratio=95
  
vm.overcommit_memory=2

Refer:
  
http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cdh\_admin\_performance.html
  
http://www.slideshare.net/technmsg/improving-hadoop-cluster-performance-via-linux-configuration
  
https://iainvlinux.wordpress.com/2014/02/16/memory-overcommit-settings/