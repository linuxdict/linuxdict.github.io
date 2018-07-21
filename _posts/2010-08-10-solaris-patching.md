---
id: 579
title: Solaris Patching
date: 2010-08-10T21:20:34+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=579
permalink: /2010-08-solaris-patching/
categories:
  - solaris
tags:
  - solaris
---
Busy with Solaris patching these days. some servers didn&#8217;t reboot/patch for more than 3 years.

Some tips:
  
1. &#8220;ERROR: LSI1030: timeout waiting for interrupt status.
  
ERROR: LSI1030 MPT Firmware, receive-message: issue-port-enable failed.&#8221;

Possible Answers:
  
1st:
  
{3} ok setenv auto-boot? false
  
{3} ok reset-all
  
{3} ok probe-scsi-all
  
sc>reset -y
  
<!--more-->


  
2nd:
  
sc>poweroff
  
sc>poweron
  
simple, right? But i fixed it in the 2nd way.
  
Possible why I guess, because the harddisk has been replaced. need to re-read by the server ?

3rd:
  
{3} ok setenv diag-level max
  
check the POST information. 

2. Fix broken meta, due to the harddisk have been replaced rudely.

#check the status.
  
metastat
  
&#8230;&#8230;.
  
d3: Mirror
      
Submirror 0: d13
        
State: **Needs maintenance**
      
Submirror 1: d23
        
State: Okay
      
Pass: 1
      
Read option: roundrobin (default)
      
Write option: parallel (default)
      
Size: 8395200 blocks (4.0 GB)

d13: Submirror of d3
      
State: Needs maintenance
      
Invoke: **metareplace d3 c1t0d0s3 <new device>**
      
Size: 8395200 blocks (4.0 GB)
      
Stripe 0:
          
Device Start Block Dbase State Reloc Hot Spare
          
c1t0d0s3 0 No Maintenance Yes

d23: Submirror of d3
      
State: Okay
      
Size: 8395200 blocks (4.0 GB)
      
Stripe 0:
          
Device Start Block Dbase State Reloc Hot Spare
          
c1t1d0s3 0 No Okay Yes
  
&#8230;&#8230;.

\# Detach the broken one
  
metadetach -f d3 d13

\# Clear the meta data
  
metaclear d13

\# Re-read the configuration, so d13 will be online
  
metainit -a

\# Re-attach it back
  
metattach d3 d13

\# Wait it rsyncing
  
&#8230;&#8230;.
  
d3: Mirror
      
Submirror 0: d13
        
State: Resyncing
      
Submirror 1: d23
        
State: Okay
      
Resync in progress: 0 % done
      
Pass: 1
      
Read option: roundrobin (default)
      
Write option: parallel (default)
      
Size: 8395200 blocks (4.0 GB)

d13: Submirror of d3
      
State: Resyncing
      
Size: 8395200 blocks (4.0 GB)
      
Stripe 0:
          
Device Start Block Dbase State Reloc Hot Spare
          
c1t0d0s3 0 No Okay Yes

d23: Submirror of d3
      
State: Okay
      
Size: 8395200 blocks (4.0 GB)
      
Stripe 0:
          
Device Start Block Dbase State Reloc Hot Spare
          
c1t1d0s3 0 No Okay Yes
  
&#8230;&#8230;.

Ref: http://www.morphosppc.com/article/repair-solaris-svm-metadevices/