---
id: 813
title: UltraMonkey-L7 Quick Setup Guides
date: 2013-08-20T00:52:01+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=813
permalink: /2013-08-ultramonkey-l7-quick-setup-guides/
categories:
  - Howto
tags:
  - HA
---
\# OS: CentOS 6.4 x86_64 with minimal installation.

\# Enable EPEL
  
rpm -ivh http://mirror.pnl.gov/epel/6/i386/epel-release-6-8.noarch.rpm

\# Install necessary packages
  
yum install -y boost-thread.x86\_64 boost-system.x86\_64 boost-regex.x86\_64 boost-serialization.x86\_64 log4cxx apr-util apr perl-IO-Socket-INET6 perl-libwww-perl perl-Time-HiRes perl-Socket6 net-snmp-libs

\# Copy the sample configuration
  
cp /etc/ha.d/conf/l7directord.cf.sample /etc/ha.d/conf/l7directord.cf
  
<!--more-->


  
\# make necessary change, basically we don&#8217;t need change too much
  
[root@cnt01 ~]# diff /etc/ha.d/conf/l7directord.cf.sample /etc/ha.d/conf/l7directord.cf
  
32,34c32,34
  
< virtual = 192.168.0.50:80 < real = 192.168.0.51:80 masq 1 < real = 192.168.0.52:80 masq 1 \--- > virtual = 192.168.1.50:80
  
> real = 192.168.1.91:80 masq 1
  
> real = 192.168.1.93:80 masq 1

\# Setup VIP
  
ifconfig eth0:0 192.168.1.50 up

\# Start L7
  
/etc/init.d/l7vsd start
  
/etc/init.d/l7directord start
  
tail -f /var/log/l7vs/l7directord.log &

\# check healthy
  
[root@cnt01 ~]# l7vsadm
  
Layer-7 Virtual Server version 3.0.4
  
Prot LocalAddress:Port ProtoMod Scheduler
    
-> RemoteAddress:Port Forward Weight ActiveConn InactConn
  
TCP 192.168.1.50:http sessionless rr
    
-> 192.168.1.91:http Masq 1 0 0
    
-> mgm01.linuxdict.com:http Masq 1 0 0 

\# Debug
  
/var/log/l7vs/ 

\# default LB use sessionless, you can change the module to ip make it session sense LB