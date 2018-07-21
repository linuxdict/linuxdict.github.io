---
id: 551
title: /var/log/lastlog file is too large?
date: 2010-05-03T21:55:49+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=551
permalink: /2010-05-varloglastlog-file-is-too-large/
bttc_cache:
  - 1273363922:0
  - 1273363922:0
categories:
  - linux
---
In Short:
  
/var/log/lastlog is a sparse file. A sparse file is a file that contains unallocated blocks or &#8220;empty space&#8221;, as it implies, it does not actually take up filesystem space. 

The size of the file /var/log/lastlog can appear to be overly large on some systems, most especially in 64 bit architectures.

ls -la /var/log/lastlog
  
-r&#8212;&#8212;&#8211; 1 root root 1254130450140 Jul 27 08:25 /var/log/lastlog

<!--more-->

From the above example, the lastlog file is reporting to be ~1.2TB in size. This file is large since it contains information regarding the last login for all users. The UID of nfsnobody on 64 bit systems is 4294967294 or 2^32 &#8211; 2, this is considered to be the last UID on the system. Some arithmetic to show how the 1TB size is reached can be found below:

4294967294 * 256 = 1099511627264 bytes

From the calculation we see above, 256 is the amount of space each UID entry takes up in the lastlog file.

This file is what we call a sparse file. A sparse file is a file that contains unallocated blocks or &#8220;empty space&#8221;, as it implies, it does not actually take up filesystem space. To test this theory, execute the following command:

du -H /var/log/lastlog
  
58KB /var/log/lastlog

Here the file is reported to be only ~6MB. This is the actual disk space the file is taking up. The lastlog file only records data for users that have logged in.

An important point to note when operating with sparse files is that certain tools do have built-in functionality to deal with these types of files. For example cp, tar and rsync. See the man page for each of those commands for further information.