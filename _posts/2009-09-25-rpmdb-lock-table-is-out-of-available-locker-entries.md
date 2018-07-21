---
id: 457
title: 'rpmdb: Lock table is out of available locker entries'
date: 2009-09-25T01:24:35+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=457
permalink: /2009-09-rpmdb-lock-table-is-out-of-available-locker-entries/
bttc_cache:
  - 1273324673:0
categories:
  - Howto
---
If up2date throws some horrible Python errors and rpm says “rpmdb: Lock table is out of available locker entries”, you can restore your system to normality with the following:

The errors:

rpmdb: Lock table is out of available locker entries
  
error: db4 error(22) from db->close: Invalid argument
  
error: cannot open Packages index using db3 &#8211; Cannot allocate memory (12)
  
error: cannot open Packages database in /var/lib/rpm

Make a backup of /var/lib/rpm in case you break something:

tar cvzf rpmdb-backup.tar.gz /var/lib/rpm

Remove the Berkeley databases that rpm uses:

rm /var/lib/rpm/__db.00*

Make rpm rebuild the databases from scratch (may take a short while):

rpm &#8211;rebuilddb

Now, check rpm to make sure everything is okay:

rpm -qa | sort

Why does this happen?
  
When rpm accesses the Berkeley database files, it makes temporary locker entries within the tables while it searches for data. If you control-c your rpm processes often, this issue will occur much sooner because the locks are never cleared.

From:
  
http://rackerhacker.com/2007/05/27/rpmdb-lock-table-is-out-of-available-locker-entries/

btw: opensuse/debian series didn&#8217;t happy that kind of problem.