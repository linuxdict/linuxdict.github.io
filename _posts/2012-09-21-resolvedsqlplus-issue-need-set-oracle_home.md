---
id: 759
title: (resolved)sqlplus issue need set oracle_home
date: 2012-09-21T23:03:48+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=759
permalink: /2012-09-resolvedsqlplus-issue-need-set-oracle_home/
categories:
  - linux
---
bash-3.2$ rpm -qa|grep oracle
  
oracle-instantclient-sqlplus-11.1.0.1-1
  
oracle-instantclient-basic-11.1.0.1-1

bash-3.2$ sqlplus
  
Error 6 initializing SQL*Plus
  
Message file sp1<lang>.msb not found
  
SP2-0750: You may need to set ORACLE_HOME to your Oracle software directory

Fix:
  
bash-3.2$ export ORACLE_HOME=/usr/lib/oracle/11.1.0.1/client64
  
bash-3.2$ export LD\_LIBRARY\_PATH=$ORACLE\_HOME/lib:$LD\_LIBRARY_PATH
  
bash-3.2$ /usr/lib/oracle/11.1.0.1/client64/bin/sqlplus erer/pass@IP:1526/SPAPA1P 

SQL*Plus: Release 11.1.0.6.0 &#8211; Production on Sat Sep 22 04:33:02 2012