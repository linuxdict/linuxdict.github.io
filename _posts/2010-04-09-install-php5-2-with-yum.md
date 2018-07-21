---
id: 537
title: Install Php5.2 with Yum
date: 2010-04-09T05:16:36+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=537
permalink: /2010-04-install-php5-2-with-yum/
bttc_cache:
  - 1273363923:0
  - 1273363923:0
categories:
  - Howto
  - LAMP
---
Install Php5.2.x with yum.
  
1. Enable development repositories on CentOS, but only for i386
  
http://wiki.centos.org/HowTos/PHP\_5.1\_To_5.2
  
2. Only for Test Enviorment, not recommend for Prod. 🙂
  
$rpm &#8211;import http://www.jasonlitka.com/media/RPM-GPG-KEY-jlitka
  
\# create /etc/yum.repos.d/utterramblings.repo
  
`$vi /etc/yum.repos.d/utterramblings.repo<br />
# paste the following lines<br />
[utterramblings]<br />
name=Jason's Utter Ramblings Repo<br />
baseurl=http://www.jasonlitka.com/media/EL$releasever/$basearch/<br />
enabled=1<br />
gpgcheck=1<br />
gpgkey=http://www.jasonlitka.com/media/RPM-GPG-KEY-jlitka`
  
$yum update php
  
http://www.jasonlitka.com/yum-repository/