---
id: 627
title: 'Solaris: Boot archive error or corrupt'
date: 2011-06-01T16:21:41+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=627
permalink: /2011-06-solaris-boot-archive-error-or-corrupt/
categories:
  - Howto
  - solaris
tags:
  - solaris
  - tips
---
Boot archive error or corrupt

A few weeks ago, I got a little problem with my solaris box, namely solaris won&#8217;t boot because the boot archive was corrupt, \*sigh\*. Anyway the boot archive in solaris 10 was contain kernel module and configuration file was needed for solaris to startup the system.

> Error:
> 
> module /platform/i86pc/boot_archive error 3 bad or corrupt data while decompressing file

Workaround:

Boot up your solaris in &#8220;solaris failsafe mode&#8221;, next solaris image will mount with writeable mode on &#8220;/a&#8221; mount point

rm -f /a/platform/i86pc/boot_archive
  
bootadm update-archive -R /a
  
reboot