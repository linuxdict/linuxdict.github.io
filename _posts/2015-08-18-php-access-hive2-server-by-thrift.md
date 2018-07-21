---
id: 888
title: php access hive2 server by thrift
date: 2015-08-18T00:31:21+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=878
permalink: /2015-08-php-access-hive2-server-by-thrift/
categories:
  - bigdata
---
You can get some guys did on https://github.com/search?utf8=%E2%9C%93&q=php+thrift+hive

When you try to access Hive2 without SASL. you may met following alerts:
  
TTransportException&#8217; with message &#8216;TSocket: timed out reading 67108844 bytes from

Try add following lines to /etc/hive/conf/hive-site.xml

> <property> <name>hive.server2.authentication</name>
      
> <value>NOSASL</value>
     
> <description>Client authentication types.
     
> NONE: no authentication check
     
> LDAP: LDAP/AD based authentication
     
> KERBEROS: Kerberos/GSSAPI authentication
     
> CUSTOM: Custom authentication provider
     
> (Use with property hive.server2.custom.authentication.class)
      
> </description> </property>
Notes: NOSASL not equal NONE. NONE is default and means Plain SASL.