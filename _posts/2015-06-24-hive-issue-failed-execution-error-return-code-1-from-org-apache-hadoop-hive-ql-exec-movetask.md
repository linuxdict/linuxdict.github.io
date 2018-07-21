---
id: 884
title: 'Hive Issue: FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.MoveTask'
date: 2015-06-24T22:01:17+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=867
permalink: /2015-06-hive-issue-failed-execution-error-return-code-1-from-org-apache-hadoop-hive-ql-exec-movetask/
categories:
  - Linux_D
tags:
  - bigdata
---
2015-06-25 11:16:52,554 INFO [main]: metastore.HiveMetaStore (HiveMetaStore.java:logInfo(623)) &#8211; 0: get\_table : db=lntest tbl=tmp\_download
  
2015-06-25 11:16:52,554 INFO [main]: HiveMetaStore.audit (HiveMetaStore.java:logAuditEvent(305)) &#8211; ugi=abcuser ip=unknown-ip-addr cmd=get_table : db=lntest tbl=
  
tmp_download
  
2015-06-25 11:16:52,555 ERROR [main]: bonecp.ConnectionHandle (ConnectionHandle.java:markPossiblyBroken(388)) &#8211; Database access problem. Killing off this connection and all r
  
emaining connections in the connection pool. SQL State = 08S01
  
2015-06-25 11:16:52,557 ERROR [main]: bonecp.BoneCP (BoneCP.java:destroyConnection(221)) &#8211; Error in attempting to close connection
  
com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: Communications link failure during rollback(). Transaction resolution unknown.
          
at sun.reflect.GeneratedConstructorAccessor114.newInstance(Unknown Source)

Problem related with MySQL for Hive settings:
   
mysql> show global variables like &#8216;%time%&#8217; ;
  
<!--more-->

update it make it something like 28800 (default)

mysql> SET GLOBAL wait_timeout = 28800;

update my.cnf to update it permanent by adding:
   
wait_timeout = 28800

Or you can set interactiveClient=true in the JDBC connection string. Which uses an alternative timeout period.