---
id: 459
title: 'rpmlib(FileDigests) <= 4.6.0-1 is needed'
date: 2009-09-27T02:16:01+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=459
permalink: /2009-09-rpmlibfiledigests/
bttc_cache:
  - 1273362687:0
categories:
  - Linux杂记
---
Maybe u met this problem when install PGSQL on CentOS 5.3
  
rpmlib(FileDigests) <= 4.6.0-1 is needed by pgdg-centos-8.5-1.noarch we check the pgsql rpm release version pgdg-centos-8.5-1.noarch [4 KiB] Changelog by Devrim GUNDUZ **(2009-08-26)**:
  
pgdg-centos-8.4-1.noarch [4 KiB] Changelog by Devrim GUNDUZ **(2008-09-03)**:
  
as far as we got, 8.5 is packaged recently, so the rpm-libs maybe very new.

to resolve this problem:

two option:
  
1. upgrade your system (rpm package)
  
as I searched, rpm 4.7.1 include rpmlib(FileDigests) <= 4.6.0-1 http://rpmfind.net//linux/RPM/fedora/devel/i386/rpm-libs-4.7.1-6.fc12.i686.html 2. install 8.4 rpm -Uvh http://yum.pgsqlrpms.org/reporpms/8.4/pgdg-centos-8.4-1.noarch.rpm btw: why the package in CentOS keep so old. coooool. OpenSUSE/Debian/Ubuntu is better in new packages