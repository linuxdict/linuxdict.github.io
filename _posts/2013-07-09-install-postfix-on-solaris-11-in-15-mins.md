---
id: 805
title: Install Postfix on Solaris 11 in 15 mins
date: 2013-07-09T17:11:35+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=805
permalink: /2013-07-install-postfix-on-solaris-11-in-15-mins/
categories:
  - solaris
tags:
  - postfix
  - solaris
---
\# Prepare compile environment
  
root@xxx:~/# cat /etc/release
  
Oracle Solaris 11.1 X86
  
root@xxx:~/# pkg install developer/gcc-45
  
root@xxx:~/# pkg install library/gnutls

\# Disable sendmail
  
root@xxx:~/# svcadm disable svc:/network/smtp:sendmail

\# get postfix from postfix sites
  
http://www.postfix.org/download.html

\# Install postfix<!--more-->


  
root@xxx:~/# tar xf postfix-2.x.x.tar.gz
  
root@xxx:~/postfix-2.10.1# cd postfix-2.x.x
  
root@xxx:~/postfix-2.10.1# gmake clean
  
root@xxx:~/postfix-2.10.1# gmake makefiles MAKE=gmake CCARGS=&#8217;-DNO\_NIS -DUSE\_TLS -lssl -lcrypto&#8217;
  
root@xxx:~/postfix-2.10.1# gmake
  
root@xxx:~/postfix-2.10.1# gmake install

\# start Postfix
  
root@xxx:~/postfix-2.10.1# postfix start

\# Test postfix
  
root@xxx:~/postfix-2.10.1# postfix status
  
root@xxx:~/postfix-2.10.1# mail -s &#8220;Test email&#8221; your\_name@your\_domain.com

\# More configuration on postfix can check http://www.postfix.org/documentation.html