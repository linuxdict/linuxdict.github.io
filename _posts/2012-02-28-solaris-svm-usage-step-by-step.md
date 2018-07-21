---
id: 723
title: Solaris SVM usage step by step
date: 2012-02-28T07:20:45+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=723
permalink: /2012-02-solaris-svm-usage-step-by-step/
categories:
  - Howto
  - solaris
tags:
  - solaris
  - tips
---
Notes: need create svm env for Prod patch test. actually zfs is much convinent now. still the requirement issue. we can&#8217;t take advantage of zfs in Solaris 9/8

Step 1.
  
create VM with 2 drives. c0t0d0 & c0t1d0

Step 2.
  
Duet to hardware limit, we use x86, Install Solaris 10 with option 4. install with Text console. we install OS on one disk

Step 3.
  
Create SVM
  
<!--more-->


  
3.1 create the same disk layout as rootdisk,
  
prtvtoc /dev/rdsk/c0t0d0s2|fmthard -s &#8211; /dev/rdsk/c0t1d0s2

3.2 initialize the metadb, depends the layout you have. choose two slice for the meta store.
  
metadb -a -f -c 2 _c0t0d0s3 c0t1d0s3_
  
metadb
          
flags first blk block count
       
a m p luo 16 8192 /dev/dsk/c0t0d0s3
       
a p luo 16 8192 /dev/dsk/c0t1d0s3

3.3 install grub to the s0 for / ? (maybe not nessary to solaris 10)
  
installgrub /boot/grub/stage1 /boot/grub/stage2 /dev/rdsk/c0t1d0s0

3.4 create mirror for /
  
\# metainit -f d10 concat/stripe numstripes slice
  
metainit -f d10 1 1 c0t0d0s0
  
metainit -f d20 1 1 c0t1d0s0

\# metainit mirror -m submirror
  
metainit d0 -m d10

\# create root on the mirror, this will update /etc/vfstab and /etc/system let the boot use d0
  
metaroot d0

3.5 after that reboot &#8212; -r, then attach d20 to the mirror.
  
metattach d0 d20

3.6. do the same on /var

Issue and tips;
  
\# mount cd on solaris
  
iostate -En #get the cdrom
  
mount -F hsfs -o ro /dev/dsk/c1t0d0s0 /mnt
  
or
  
mount -F hsfs -r /dev/sr0 /mnt

\# swap off the swap device
  
swap -d /dev/dsk/c0t0d0sx