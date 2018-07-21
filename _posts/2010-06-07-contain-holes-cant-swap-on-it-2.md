---
id: 876
title: 'contain holes &#8211; can&#039;t swap on it.'
date: 2010-06-07T21:16:05+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=569
permalink: /2010-06-contain-holes-cant-swap-on-it-2/
categories:
  - solaris
tags:
  - solaris
  - tips
---
root@home# mkfile 512m /var/swapfile
  
root@home# swap -a /var/swapfile
  
&#8220;/var/swapfile&#8221; may contain holes &#8211; can&#8217;t swap on it.

the above is ok for UFS, but not work in ZFS.

Solution:
  
root@home# zfs create -V 1gb rpool/swapfile
  
root@home# swap -a /dev/zvol/dsk/rpool/swapfile

Good articles on Swap
  
http://blogs.sun.com/jimlaurent/entry/solaris\_faq\_myths\_and\_facts