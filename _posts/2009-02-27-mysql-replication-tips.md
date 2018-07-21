---
id: 240
title: MySQL Replication Tips
date: 2009-02-27T22:43:13+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=240
permalink: /2009-02-mysql-replication-tips/
bttc_cache:
  - 1273284809:0
  - 1273284809:0
categories:
  - LAMP
---
MySQL的Replication已经很成熟了。下面总结一下生产中的一些小技巧

1、从Master上来过滤一些数据库，即忽略test,scratch数据库，不进行Rep
  
binlog-ignore-db=test,scratch
  
或者
  
binlog-ignore-db=test
  
binlog-ignore-db=scratch

2、如果只想同步某一或几个数据库，可以只制定需要Repl的数据库名
  
binlog-do-db=catalog
  
binlog-do-db=users
  
binlog-do-db=sessions

3、如果某些SQL语句导致Repl出现问题，可以使用如下方法：
  
SET GLOBAL SQL\_SLAVE\_SKIP_COUNTER = 1;
  
SLAVE START SQL_THREAD;

4、从Slaves上过滤数据库，只同步某一些数据库（users）。
  
replicate-do-db=users
  
阻止temporary数据库同步的设置方法：
  
replicate-ignore-db=temporary