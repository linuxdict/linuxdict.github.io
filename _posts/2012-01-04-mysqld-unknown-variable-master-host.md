---
id: 704
title: 'mysqld: unknown variable &#8216;master-host='
date: 2012-01-04T22:42:45+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=704
permalink: /2012-01-mysqld-unknown-variable-master-host/
categories:
  - MySQL知识库
---
Are you trying to setup on replication on mysql5.5+ ? ok. then that&#8217;s the issue. 

The following options are removed in MySQL 5.5. If you attempt to start mysqld with any of these options in MySQL 5.5, the server aborts with an unknown variable error.

&#8211;master-host
  
&#8211;master-user
  
&#8211;master-password
  
&#8211;master-port

Solution, comment the master- related variables.<!--more-->


  
Do following,
  
On Master:
  
mysql>GRANT REPLICATION SLAVE ON \*.\* TO &#8216;slave_user&#8217;@&#8217;%&#8217; IDENTIFIED BY &#8216;<some_password>&#8216;; (Replace <some_password> with a real password!)
  
mysql>FLUSH PRIVILEGES;
  
mysql>FLUSH TABLES WITH READ LOCK;
  
mysql>SHOW MASTER STATUS;
  
\# get the DB dump.
  
mysql>UNLOCK TABLES;

On Slave:
  
\# import the DB dump
  
mysql>stop slave;
  
mysql>CHANGE MASTER TO MASTER\_HOST=&#8217;prod\_master&#8217;, MASTER\_USER=&#8217;slave\_user&#8217;, MASTER_PASSWORD=&#8217;<some\_password>&#8216;, MASTER\_LOG_FILE=&#8217;_mysql-bin.0xx_&#8216;, MASTER\_LOG\_POS=_33421_;
  
mysql>start slave;

Ref: http://dev.mysql.com/doc/refman/5.5/en/replication-options-slave.html