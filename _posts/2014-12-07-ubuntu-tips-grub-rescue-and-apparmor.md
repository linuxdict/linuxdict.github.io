---
id: 854
title: 'Ubuntu tips: grub rescue and apparmor'
date: 2014-12-07T12:18:10+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=854
permalink: /2014-12-ubuntu-tips-grub-rescue-and-apparmor/
categories:
  - linux
tags:
  - tips
  - Ubuntu
---
Installed Ubuntu on Old laptop for testing new thing like Docker. met 2 issue. 

Issue 1. Update the disk partition table caused the grub confused.
  
I have 4 slice of my harddisk, /dev/sda1 for Windows. /dev/sda5 for windows 2nd partition. /dev/sda6 for Ubuntu./dev/sda7 for Ubuntu swap.
  
when I need more space for linux, I remove /dev/sda5. then /dev/sda6 become /dev/sda5 &#8230;. that confused grub. because grub still hold the record /dev/sda6 is the linux partition. 

Fix: grub rescue>ls
       
grub rescue>set
  
<!--more-->

change the prefix and the root from (hd0,msdos6) to (hd0,msdos5)
       
grub rescue>insmod /boot/grub/i386-pc/normal.mod
       
grub rescue>normal
  
Then you got my grub back , boot into Ubuntu and then run sudo update-grub2 , grub.cfg should be updated. 

Issue 2. Apparmor issue, when I try to migrate mysql data to /data/mysql. found the mysql won&#8217;t start

it keeps complains:
  
/usr/sbin/mysqld: Can&#8217;t find file: &#8216;./mysql/plugin.frm&#8217; (errno: 13)
  
141207 17:02:29 [ERROR] Can&#8217;t open the mysql.plugin table. Please run mysql_upgrade to create it.
  
141207 17:02:29 InnoDB: The InnoDB memory heap is disabled
  
&#8230;..
  
InnoDB: The error means mysqld does not have the access rights to
  
InnoDB: the directory.
  
InnoDB: File name ./ibdata1
  
InnoDB: File operation call: &#8216;open&#8217;.
  
InnoDB: Cannot continue operation.

finally turn out it&#8217;s Apparmor which like SElinux.
  
sudo apparmor_status
     
/usr/sbin/mysqld

Fix: add the data directory to the apparmor policy file.
  
/etc/apparmor.d/usr.sbin.mysqld

/data/mysql/ r,
    
/data/mysql/** rwk,