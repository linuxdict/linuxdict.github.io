---
id: 890
title: '(Fixed) I/O error trying to sync with MASTER: connection lost'
date: 2015-08-26T01:05:37+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=886
permalink: /2015-08-fixed-io-error-trying-to-sync-with-master-connection-lost/
categories:
  - Howto
tags:
  - redis
---
Error:

[2162] 26 Aug 15:26:26.795 # I/O error trying to sync with MASTER: connection lost

Above error happened when there is poor network connection, and you do the slave sync first time.

Possible Solution: increase slave buffer from 256m 64m 60 to 512M 128m 120

x.x.x.x:6379> config get client-output-buffer-limit
  
1) &#8220;client-output-buffer-limit&#8221;
  
2) &#8220;normal 0 0 0 slave 268435456 67108864 60 pubsub 33554432 8388608 60&#8221;
  
<!--more-->

x.x.x.x:6379> config set client-output-buffer-limit &#8220;normal 0 0 0 slave 536870912 134217728 120 pubsub 33554432 8388608 60&#8221;

x.x.x.x:6379> config get client-output-buffer-limit

2) &#8220;normal 0 0 0 slave 536870912 134217728 120 pubsub 33554432 8388608 60&#8221;

Once your first sync completed. you can rollback the setting.

Refer: http://redis.io/topics/clients