---
id: 400
title: Update Ubuntu with Approx
date: 2009-07-15T03:02:35+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=400
permalink: /2009-07-update-ubuntu-with-approx/
bttc_cache:
  - 1273344709:0
  - 1273344709:0
categories:
  - Howto
tags:
  - server
  - tips
---
Read some articles on Ubuntu recently. 

occasionally read an article about approx, It works like a cache server. can cache the *.deb for other usage

the approx server: run sudo apt-get install approx
  
/etc/approx/approx.conf :
  
&#8212;&#8211;start&#8212;&#8212;&#8212;
  
ubuntu http://us.archive.ubuntu.com/ubuntu
  
security http://security.ubuntu.com/ubuntu
  
canonical http://archive.canonical.com/ubuntu
  
&#8212;&#8211;stop&#8212;&#8212;&#8212;
  
sudo /etc/init.d/approx start
  
if u has firewall, open port 9999

the clients: sudo mv /etc/atp/source.list /etc/atp/source.list.orgin
  
sudo vi /etc/atp/source.list
  
paste the following lines
  
(**note**: change SID to ur release )
  
deb http://approx\_server\_ip:9999/ubuntu/ _intrepid_ main restricted universe multiverse
  
deb http://approx\_server\_ip:9999/buntu/ _intrepid_-updates universe multiverse
  
deb http://approx\_server\_ip:9999/ubuntu _intrepid_-security main restricted universe multiverse