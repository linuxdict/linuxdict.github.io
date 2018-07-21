---
id: 885
title: Migrate existing hadoop to CDH
date: 2015-07-07T23:09:59+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=869
permalink: /2015-07-migrate-existing-hadoop-to-cdh/
categories:
  - Howto
  - linux
tags:
  - hadoop
---
Don&#8217;t need to sell CDH&#8217;s benefits. you should know it before want to migrate 🙂

Very Important, The following has been tested in my lab, all goes fine. can&#8217;t grantee if also works for you.
  
I migrate from Apache Hadoop 2.2 to CDH 5.3 or 5.4 all works.

\## Backup namenode
  
\# cd /mnt/hadoop/hdfs/name
  
\# tar -cvf /root/nn\_backup\_data.tar .

.
  
./current/fsimage
  
..
  
./current/edits
  
./image/
  
./image/fsimage

\## Install CDH WITHOUT create any service.
  
<!--more-->


  
\## Create HDFS service.
  
Important: your NN or DN data directory must match existing Hadoop. don&#8217;t worry, CDH won&#8217;t format/clean your existing data.

\## Stop existing Hadoop, do HDFS metadata upgrade.
  
Option1: Cloudera Manager GUI.
  
HDFS->Upgrade HDFS Metadata-> Finalize Metadata Upgrade

Option2: login NN.
  
hdfs namenode -upgrade

\## Start HDFS from CM GUI now.

Issue you may meet during Migration:

Issue1:
  
2015-07-23 13:54:04,150 ERROR org.apache.hadoop.hdfs.server.namenode.NameNode: Failed to start namenode.
  
org.apache.hadoop.hdfs.server.common.InconsistentFSStateException: Directory /data/hadoop/hdfs/name is in an inconsistent state: previous fs state should not exist during upgrade. Finalize or rollback first.
          
at org.apache.hadoop.hdfs.server.namenode.FSImage.checkUpgrade(FSImage.java:349)
          
at org.apache.hadoop.hdfs.server.namenode.FSImage.checkUpgrade(FSImage.java:356)
          
at org.apache.hadoop.hdfs.server.namenode.FSImage.doUpgrade(FSImage.java:376)
          
at org.apache.hadoop.hdfs.server.namenode.FSImage.recoverTransitionRead(FSImage.java:268)
          
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFSImage(FSNamesystem.java:1061)
          
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFromDisk(FSNamesystem.java:765)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.loadNamesystem(NameNode.java:584)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.initialize(NameNode.java:643)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:810)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:794)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1487)
          
at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1553)
  
2015-07-23 13:54:04,152 INFO org.apache.hadoop.util.ExitUtil: Exiting with status 1
  
2015-07-23 13:54:04,179 INFO org.apache.hadoop.hdfs.server.namenode.NameNode: SHUTDOWN_MSG:

\# This may caused by Last upgrade didn&#8217;t complete.
  
hdfs dfsadmin -finalizeUpgrade

\# Issue2 : This may happened when you do HA for HDFS.
  
2015-07-23 14:28:16,082 INFO org.mortbay.log: Stopped HttpServer2$SelectChannelConnectorWithSafeStartup@master.xxxx:50070
  
2015-07-23 14:28:16,183 INFO org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping NameNode metrics system&#8230;
  
2015-07-23 14:28:16,183 INFO org.apache.hadoop.metrics2.impl.MetricsSystemImpl: NameNode metrics system stopped.
  
2015-07-23 14:28:16,183 INFO org.apache.hadoop.metrics2.impl.MetricsSystemImpl: NameNode metrics system shutdown complete.
  
2015-07-23 14:28:16,183 ERROR org.apache.hadoop.hdfs.server.namenode.NameNode: Failed to start namenode.
  
java.io.IOException: Gap in transactions. Expected to be able to read up until at least txid 46291115 but unable to find any edit logs containing txid 46291058
	  
at org.apache.hadoop.hdfs.server.namenode.FSEditLog.checkForGaps(FSEditLog.java:1537)
	  
at org.apache.hadoop.hdfs.server.namenode.FSEditLog.selectInputStreams(FSEditLog.java:1495)
	  
at org.apache.hadoop.hdfs.server.namenode.FSImage.loadFSImage(FSImage.java:644)
	  
at org.apache.hadoop.hdfs.server.namenode.FSImage.doUpgrade(FSImage.java:379)

scp slave3:/data1/hadoop/hdfs/name/current/edits\_inprogress\_0000000000046291058 /tmp/
  
sudo su &#8211; hdfs
  
-bash-4.3$ cp /tmp/edits\_inprogress\_0000000000046291058 /data1/hadoop/hdfs/name/current/edits\_inprogress\_0000000000046291058
  
-bash-4.3$ ll /data1/hadoop/hdfs/name/current/edits\_inprogress\_0000000000046291058
  
-rw-rw-r&#8211; 1 hdfs hdfs 1048576 Jul 23 14:31 /data1/hadoop/hdfs/name/current/edits\_inprogress\_0000000000046291058