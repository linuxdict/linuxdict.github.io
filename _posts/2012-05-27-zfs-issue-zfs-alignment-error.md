---
id: 736
title: 'zfs issue: zfs: alignment error ?'
date: 2012-05-27T22:24:18+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=736
permalink: /2012-05-zfs-issue-zfs-alignment-error/
categories:
  - solaris
---
Issue log:
  
Mounting ZFS filesystems: (1/15)
  
panic[cpu31]/thread=30023ee3800: BAD TRAP: type=34 rp=2a103a46890 addr=7020726573706f76 mmu_fsr=0

zfs: alignment error:
  
addr=0x7020726573706f76
  
pid=4838, pc=0x7a24d504, sp=0x2a103a46131, tstate=0x4480001600, context=0x42
  
g1-g7: 0, feedfacefeedface, feedface, 0, 3000638d940, 42, 30023ee3800

000002a103a465b0 unix:die+9c (34, 2a103a46890, 7020726573706f76, 0, 2a103a46670, c1e00000)

Solution:
  
go to single user mode.
  
ok. try &#8220;canmount=noauto&#8221; don&#8217;t automatically mount zfs.
  
<!--more-->


  
for i in \`zfs list|grep /|grep -v swap|awk &#8216;{print $1}&#8217;\`;do zfs set canmount=noauto $i;done
  
then init 3. it works.

now try manually mount one by one. you may know which caused the crash. if none report crashed. don&#8217;t read following lines.

hmm, crashed when try mount localpool/some_disk . others fine. if you don&#8217;t have important files. Be CareFul when you do created, i don&#8217;t grantee your Data.

Warning: Data lost. You&#8217;d better know what u are doing!!!!
  
zfs destroy localpool/some_disk
  
zfs create -o mountpoint=/mymnt localpool/some_disk
  
zfs set quota=3g localpool/some_disk

now try mount all the zfs. works fine.

change the mount to automatically mount.
  
for i in \`zfs list|grep /|grep -v swap|awk &#8216;{print $1}&#8217;\`;do zfs set canmount=on $i;done