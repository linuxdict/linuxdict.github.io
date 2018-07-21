---
id: 622
title: 'short scripts: convert squid timestamp'
date: 2011-05-16T21:03:48+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=622
permalink: /2011-05-short-scripts-convert-squid-timestamp/
categories:
  - Howto
  - linux
tags:
  - tips
---
cat > /var/convert.pl
  
`#!/usr/bin/perl -p<br />
s/^\d+\.\d+/localtime $&/e;`
  
Ctrl+D
  
. /var/convert.pl /var/squid/log/access.log |more