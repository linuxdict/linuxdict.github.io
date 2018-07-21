---
id: 272
title: 'I just try to rebuild the squid3 for ope&#8230;'
date: 2009-04-22T02:58:29+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=272
permalink: /2009-04-i-just-try-to-rebuild-the-squid3-for-ope/
bttc_cache:
  - 1273203999:0
  - 1273203999:0
categories:
  - Linux_D
tags:
  - squid
---
I just try to rebuild the squid3 for opensuse, i changed the filedescriptor and threads
  
modified squid3.spec
  
edit the following line about line 273
  
export CFLAGS=&#8221;$RPM\_OPT\_FLAGS -DNUMTHREADS=32 -fPIE -fPIC -fno-strict-aliasing&#8221;

and the following line on line 315
          
&#8211;with-filedescriptors=8192 

Install Requires Packages:
  
sudo zypper install krb5-devel libxml2-devel openldap2-devel opensp-devel pam-devel db-devel
  
patch autoreconf make libexpat-devel libtool

<!--more-->

some errors: (E=Errors, A=Answers)
  
E:
  
+ autoreconf -fi
  
configure.in:32: error: possibly undefined macro: AC\_DISABLE\_SHARED
        
If this token and others are legitimate, please use m4\_pattern\_allow.
        
See the Autoconf documentation.
  
configure.in:33: error: possibly undefined macro: AC\_PROG\_LIBTOOL
  
configure.in:34: error: possibly undefined macro: AC\_LTDL\_DLLIB
  
autoreconf: /usr/bin/autoconf failed with exit status: 1
  
A:
  
sudo zypper install libtool

and then:
  
rpmbuild -bb squid3.spec 

finally I got the rpm
  
/usr/src/packages/RPMS/x86\_64/squid3-3.0.STABLE9-5.1.x86\_64.rpm