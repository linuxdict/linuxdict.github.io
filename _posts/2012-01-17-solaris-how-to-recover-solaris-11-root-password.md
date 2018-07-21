---
id: 707
title: 'solaris: how to recover solaris 11 root password'
date: 2012-01-17T19:38:08+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=707
permalink: /2012-01-solaris-how-to-recover-solaris-11-root-password/
categories:
  - solaris
tags:
  - solaris
---
boot net -s
  
boot cdrom -s, if it ask username: root/solaris or root/password.

on x86, you need edit grub and append -s on kernel line.

after login. mount /dev/dsk/_cxtxdxsx_ /a

if you use zfs for /, then zfs import
  
zfs list
  
zfs set mountpoint=/a _rpool/ROOT/solaris_
  
zfs mount _-f rpool/ROOT/solaris_
  
then edit /etc/shadow
  
remove the password section, let it looks likes.
  
root::15356::::::

don&#8217;t forget to reset the mountpoint back
  
zfs set mountpoint=/ _rpool/ROOT/solaris_

reboot.