---
id: 887
title: (fixed) sqoop import from Oracle to Hive throw Heap size error
date: 2015-08-07T00:43:01+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=876
permalink: /2015-08-fixed-sqoop-import-from-oracle-to-hive-throw-heap-size-error/
categories:
  - bigdata
tags:
  - bigdata
---
If you use CDH and Sqoop. you probably met following issue:

15/08/07 15:21:55 INFO manager.SqlManager: Using default fetchSize of 1000
  
15/08/07 15:21:55 INFO tool.CodeGenTool: Beginning code generation
  
15/08/07 15:21:56 INFO manager.OracleManager: Time zone has been set to GMT
  
15/08/07 15:21:56 INFO manager.SqlManager: Executing SQL statement: select xxx where (1 = 0)
  
Exception in thread &#8220;main&#8221; java.lang.OutOfMemoryError: Java heap space
	  
at java.lang.reflect.Array.newArray(Native Method)
	  
at java.lang.reflect.Array.newInstance(Array.java:70)
	  
at oracle.jdbc.driver.BufferCache.get(BufferCache.java:226)
	  
at oracle.jdbc.driver.PhysicalConnection.getCharBuffer(PhysicalConnection.java:7698)
	  
at oracle.jdbc.driver.OracleStatement.prepareAccessors(OracleStatement.java:1013)
	  
at oracle.jdbc.driver.T4CTTIdcb.receiveCommon(T4CTTIdcb.java:277)

This related with HDFS client HEAP settings. you can fix it by increase HEAP size for HDFS client.

from CDH:
  
Client Java Heap Size in Bytes.
  
<!--more-->

or manually update hadoop-env.sh. default is 256M. you can increase -Xmx to whatever you want.
  
diff /etc/hadoop/conf/hadoop-env.sh /etc/hadoop/conf/hadoop-env.shold
  
61c61
  
< export HADOOP\_CLIENT\_OPTS="-Xms268435456 -Xmx1268435456 -Djava.net.preferIPv4Stack=true $HADOOP\_CLIENT\_OPTS" \--- > export HADOOP\_CLIENT\_OPTS=&#8221;-Xms268435456 -Xmx268435456 -Djava.net.preferIPv4Stack=true $HADOOP\_CLIENT\_OPTS&#8221;