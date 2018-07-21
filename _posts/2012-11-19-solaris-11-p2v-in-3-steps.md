---
id: 779
title: solaris 11, p2v in 3 steps
date: 2012-11-19T23:37:33+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=779
permalink: /2012-11-solaris-11-p2v-in-3-steps/
categories:
  - solaris
tags:
  - solaris
---
p2v is not a new feature. but i just tried it. 

p2v is physical to virtual. which means you can migrate solaris from real HW to solaris zone.

1. create zone on solaris11.
  
<!--more-->


  
root@bnsol11a:~# zonecfg -z liuedy-z10
  
Use &#8216;create&#8217; to begin configuring a new zone.
  
zonecfg:liuedy-z10> create -b
  
zonecfg:liuedy-z10> set brand=solaris10
  
zonecfg:liuedy-z10> set zonepath=/zone/liuedy-z10
  
zonecfg:liuedy-z10> set autoboot=true
  
zonecfg:liuedy-z10> add net
  
zonecfg:liuedy-z10:net> set address=10.240.3.180
  
zonecfg:liuedy-z10:net> set physical=net0
  
zonecfg:liuedy-z10:net> end
  
zonecfg:liuedy-z10> info
  
zonename: liuedy-z10
  
zonepath: /zone/liuedy-z10
  
brand: solaris10
  
autoboot: true
  
bootargs:
  
pool:
  
limitpriv:
  
scheduling-class:
  
ip-type: exclusive
  
hostid:
  
fs-allowed:
  
net:
	  
address: 10.240.3.180
	  
allowed-address not specified
	  
configure-allowed-address: true
	  
physical: net0
	  
defrouter not specified
  
zonecfg:liuedy-z10> verify
  
net: address cannot be specified if ip-type = exclusive
  
ip-type is set to &#8216;exclusive&#8217; by default.
  
liuedy-z10: Invalid argument
  
zonecfg:liuedy-z10> set ip-type=shared
  
zonecfg:liuedy-z10> verify
  
zonecfg:liuedy-z10> commit
  
zonecfg:liuedy-z10> exit
  
root@bnsol11a:~# zoneadm list -civ
    
ID NAME STATUS PATH BRAND IP
     
0 global running / solaris shared
     
&#8211; liuedy-z10 configured /zone/liuedy-z10 solaris10 shared

2. create flash archive of old solaris.
  
// -S don&#8217;t cacluate the archive size. -L method cpio
  
[root@beisoltest02 ~]# flarcreate -S -n sol10\_new -L cpio /net/10.240.3.210/export/zone/flash\_store/sol10_new.flar
  
Archive format requested is cpio
  
Full Flash
  
Checking integrity&#8230;
  
Integrity OK.
  
Running precreation scripts&#8230;
  
Precreation scripts done.
  
Creating the archive&#8230;
  
2464714 blocks
  
Archive creation complete.
  
Running postcreation scripts&#8230;
  
Postcreation scripts done.
  
Running pre-exit scripts&#8230;
  
Pre-exit scripts done.
  
[root@beisoltest02 ~]# 

3. install the zone

root@bnsol11a:~# zoneadm -z liuedy-z10 install -p -a /export/zone/flash\_store/sol10\_new.flar
  
Progress being logged to /var/log/zones/zoneadm.20121120T061159Z.liuedy-z10.install
      
Installing: This may take several minutes&#8230;
  
Postprocessing: This may take a while&#8230;
     
Postprocess: Updating the image to run within a zone
     
Postprocess: Migrating data
          
from: rpool/export/zone/liuedy-z10/rpool/ROOT/zbe-0
            
to: rpool/export/zone/liuedy-z10/rpool/export
     
Postprocess: A backup copy of /export is stored at /export.backup.20121120T061735Z.
  
It can be deleted after verifying it was migrated correctly.

Result: Installation completed successfully.
  
Log saved in non-global zone as /export/zone/liuedy-z10/root/var/log/zones/zoneadm.20121120T061159Z.liuedy-z10.install
  
root@bnsol11a:~# zoneadm list -civ
    
ID NAME STATUS PATH BRAND IP
     
0 global running / solaris shared
     
&#8211; liuedy-z10 installed /export/zone/liuedy-z10 solaris10 shared
  
root@bnsol11a:~# zoneadm -z liuedy-z10 boot
  
root@bnsol11a:~# zoneadm list -civ
    
ID NAME STATUS PATH BRAND IP
     
0 global running / solaris shared
     
5 liuedy-z10 running /export/zone/liuedy-z10 solaris10 shared
  
root@bnsol11a:~# zlogin -C liuedy-z10
  
[Connected to zone &#8216;liuedy-z10&#8217; console]

beisoltest02 console login: 

Issue met before.
  
Postprocessing: This may take a while&#8230;
     
Postprocess: Updating the image to run within a zone
     
Postprocess: ERROR: SMF repository unavailable.
     
Postprocess: ERROR: Failed to boot zone to single user mode.
     
Postprocess: ERROR: Postprocessing failed.
          
Result: Postprocessing failed.

this is caused by the patch level doesn&#8217;t match the necessary for migration. so it&#8217;s a good idea to keep the system up to date.
  
upgrade from SunOS 5.10/Generic\_137138-09 to Generic\_147441-25 fixed the issue.