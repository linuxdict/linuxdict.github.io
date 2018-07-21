---
id: 714
title: 'Ruby: Cipher is not a module'
date: 2012-02-05T16:25:18+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=714
permalink: /2012-02-ruby-cipher-is-not-a-module/
categories:
  - Howto
tags:
  - centos
  - ruby
---
This mostly happened on CentOS 64

Solution:
  
rpm -qi ruby
  
Name : ruby Relocations: (not relocatable)
  
Version : 1.8.7.299 Vendor: AegisCo
  
then get the source package with the same version.
  
cd /usr/src/redhat/SOURCES/ruby-1.8.7-p299/ext/openssl/
  
ruby extconf.rb
  
make
  
make install