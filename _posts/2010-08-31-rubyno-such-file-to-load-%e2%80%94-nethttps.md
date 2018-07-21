---
id: 584
title: Ruby:no such file to load — net/https
date: 2010-08-31T06:10:03+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=584
permalink: '/2010-08-rubyno-such-file-to-load-%e2%80%94-nethttps/'
categories:
  - Howto
---
gem\_original\_require’: no such file to load — net/https (MissingSourceFile) 

If you get this error when getting your app up and running under Ubuntu it means you still need to install the libopenssl-ruby library:

sudo apt-get install libopenssl-ruby