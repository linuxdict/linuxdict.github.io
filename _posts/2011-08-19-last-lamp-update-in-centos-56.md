---
id: 689
title: Last LAMP update in CentOS 5/6
date: 2011-08-19T04:24:17+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=689
permalink: /2011-08-last-lamp-update-in-centos-56/
categories:
  - LAMP
tags:
  - LAMP
---
PowerStack is a repository that allows you to run the latest LAMP versions in your Enterprise Linux. Currently both CentOS and RHEL are supported (i686 and x86_64).

rpm -Uvh http://download.powerstack.org/powerstack-release-0-2.noarch.rpm
  
yum update php 

From http://wiki.powerstack.org/PowerStack

It&#8217;s a very cool project, thanks for the developers.