---
id: 286
title: Conclusion of Optimize Squid for Reverse Proxy
date: 2009-04-23T01:39:45+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=286
permalink: /2009-04-conclusion-of-optimize-squid-for-reverse/
bttc_cache:
  - 1273290412:0
  - 1273290412:0
categories:
  - Linux_D
tags:
  - server
---
Conclusion of Optimize Squid for Reverse Proxy:

After having read and tested the guides from the articles, I got some tips on the topic:

1. recompile the squid if you can, tuning the compile parameters.
  
#ulimit -n8192 (system setting)
  
./configure &#8230; –with-filedescriptors=8192 &#8230;
  
of course the 8192 is just my parameters. if your hardware is more powerful, just increase it to handle more concurrence requests. the max is 65535 

2. squid.conf
  
cache_mem = 70-90% physical memory #if your server just for squid
  
maximum\_object\_size 1024KB #we just cache some small things just as js/css/jpg/gif.
  
maximum\_object\_size\_in\_memory 1024KB

#aufs is for async-io, offload disk reads to a thread. big cache is always good.
  
cache_dir aufs /var/spool/squid 50000 16 256
  
#cache_dir ufs Directory-Name Mbytes L1 L2 [options] L1 means 16 subdirectories L2 means 256 subdirecotries. if you don&#8217;t have good reason, just leave it.

#don&#8217;t cache 404&#8217;s, always go to origin servers
  
negative_ttl 0 minutes

#ignore the store logs
  
cache\_store\_log none

half\_closed\_clients off 

3. /var/spool/squid
  
set a individual partition for cache disk.
  
suggest to choose reiserfs file system.
  
mount -t defaults,noatime # esp noatime