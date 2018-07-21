---
id: 539
title: 'Yum Repo problem : primary.sqlite.bz2: [Errno -1]'
date: 2010-04-21T01:16:02+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=539
permalink: /2010-04-yum-repo-problem-primary-sqlite-bz2-errno-1/
bttc_cache:
  - 1273363923:0
  - 1273363923:0
categories:
  - Howto
  - linux
---
This proble happened a lot recently, no idea what&#8217;s wrong with CentOS.

updates/primary_db | 687 kB 00:02
  
http://mirror.nus.edu.sg/centos/5/updates/x86_64/repodata/primary.sqlite.bz2: [Errno -1] Metadata file does not match checksum

I try to clean the cache, but still doesn&#8217;t work

Solution: Remove the following lines in /var/cache/yum/updates/repomd.xml

<data type=&#8221;primary_db&#8221;>

<location href=&#8221;repodata/primary.sqlite.bz2&#8243;/>

<checksum type=&#8221;sha&#8221;>d36796c21c77035e68c2ae2e7dc486d75d4659cd</checksum>

<timestamp>1269791791</timestamp>

<open-checksum type=&#8221;sha&#8221;>5c914da1b9b979b2097ff69062ca21783d5190d7</open-checksum>

<database\_version>10</database\_version>

</data>