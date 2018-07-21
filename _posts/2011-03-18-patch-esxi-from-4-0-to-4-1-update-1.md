---
id: 616
title: Patch ESXi from 4.0 to 4.1 Update 1
date: 2011-03-18T21:31:08+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=616
permalink: /2011-03-patch-esxi-from-4-0-to-4-1-update-1/
categories:
  - Howto
---
Target: Patch ESXi from 4.0 to 4.1 Update 1
  
Preparation: Install vSphere Client

1st round
  
\# halt all the VMs from Vsphpere

\# put the ESXi into &#8220;maintenance mode&#8221;, right click the host.

\# backup the firmware configuration
  
C:\Program Files\VMware\VMware vSphere CLI\bin>vicfg-cfgbackup.pl &#8211;server beivm
  
srv01 -s beivmsrv01_20110320.bak
  
Enter username: root
  
Enter password:
  
Saving firmware configuration to beivmsrv01_20110320.bak &#8230;

<!--more-->


  
\# update from 4.0 to 4.1
  
C:\Program Files\VMware\VMware vSphere CLI\bin>vihostupdate.pl &#8211;server beivmsrv
  
01 -i -b F:\ISO\upgrade-from-ESXi4.0-to-4.1.0-0.0.260247-release.zip
  
Enter username: root
  
Enter password:
  
Please wait patch installation is in progress &#8230;
  
The update completed successfully, but the system needs to be rebooted for the c
  
hanges to be effective.

\# check the patch
  
C:\Program Files\VMware\VMware vSphere CLI\bin>vihostupdate.pl &#8211;server beivmsrv
  
01 &#8211;query
  
Enter username: root
  
Enter password:
  
&#8212;&#8212;&#8212;Bulletin ID&#8212;&#8212;&#8212; &#8212;&#8211;Installed&#8212;&#8211; &#8212;&#8212;&#8212;&#8212;&#8212;-Summary&#8212;&#8212;-
  
&#8212;&#8212;&#8212;-
  
ESXi410-GA 2010-10-03T07:10:52 ESXi upgrade Bulletin

ESXi410-GA-esxupdate 2010-10-03T07:10:52 ESXi pre-upgrade Bulletin

\# use vsphere to reboot 

2nd round
  
\# put the ESXi into &#8220;maintenance mode&#8221;, if the host is not in that mode, right click the host.

\# update from 4.1 to 4.1 update 1
  
C:\Program Files\VMware\VMware vSphere CLI\bin>vihostupdate.pl &#8211;server beivmsrv
  
01 -i -b F:\ISO\update-from-esxi4.1-4.1_update01.zip
  
Enter username: root
  
Enter password:
  
Please wait patch installation is in progress &#8230;
  
The update completed successfully, but the system needs to be rebooted for the c
  
hanges to be effective.

\# use vsphere to reboot