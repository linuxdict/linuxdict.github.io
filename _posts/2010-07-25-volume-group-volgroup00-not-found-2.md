---
id: 877
title: 'Volume group &quot;VolGroup00&quot; not found'
date: 2010-07-25T20:15:18+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=576
permalink: /2010-07-volume-group-volgroup00-not-found-2/
categories:
  - Howto
  - linux
tags:
  - tips
  - virtualbox
---
Met a problem when try to copy virtualbox vdi file directly from Windows virtualbox to Linux

&#8220;Error: Volume group &#8220;VolGroup00&#8243; not found
  
&#8230;&#8230;
  
Kernel panic &#8211; not syncing: Attempted to kill init!&#8221;

Solution:
  
First, boot up in rescue mode, using the CentOS cd, type &#8220;linux rescue&#8221; on the first boot prompt.

Now chroot to you actual system:
  
#chroot /mnt/sysimage

Then, backup your initrd:
  
#cd /boot
  
#mv initrd-2.6.18-164.el5.img initrd.backup

(use the last version, or the one you are trying to boot, on the &#8220;2.6.18-92.el5.img&#8221; part)
  
Now rebuild your initrd:

#mkinitrd /boot/initrd-2.6.18-164.el5.img 2.6.18-164.el5
  
(Same thing about the versions)

#reboot