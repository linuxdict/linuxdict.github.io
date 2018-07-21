---
id: 635
title: /var/adm/wtmpx too big
date: 2011-07-07T18:06:20+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=635
permalink: /2011-07-varadmwtmpx-too-big/
categories:
  - solaris
tags:
  - tips
---
How to safely clean the /var/adm/wtmpx

Solution 1 (clean everything):
  
\# cd /var/adm
  
\# gzip -c wtmpx > wtmpx.backup.gz
  
\# > wtmpx

Solution 2(keep last 1000 logs):
  
\# cd /var/adm
  
\# /usr/lib/acct/fwtmp < wtmpx | tail -1000 > wtmpx.ascii
  
\# /usr/lib/acct/fwtmp -ic < wtmpx.ascii > wtmpx
  
\# rm wtmpx.ascii
  
The commands makes convert info from binary to ascii from wtmpx, save last 1000 lines into wtmpx.ascii file, convert the info in wtmpx.ascii to binary again, and save it into wtmpx. Finally no-needed wtmpx.ascii is removed.