---
id: 827
title: Veritas Cluster Server CP server install and configuration guide
date: 2013-12-03T22:25:44+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=827
permalink: /2013-12-veritas-cluster-server-cp-server-install-and-configuration-guide/
categories:
  - Howto
tags:
  - vcs
---
When you read this article, i assume you already know the split-brain issue in Cluster. VCS have CP server to avoid the split-brain issue. also you can use SCSI3-PR func if your SAN storage support that. 

We mainly focus on CP server setup and Configure the cluster to use CP servers. 

=== Part 1, Setup CPS server ===
  
CP server setup. you can install SFHA all package. which include the CPS server

VRTScps All Cluster Server &#8211; Coordination Point Server

\# Quick Steps:
  
/opt/VRTS/install/installvcs61 -configcps

\# Manual Steps without VCS, because CPS can run alone.
  
\# Once you installed, create CPS configuration.
  
`<br />
root@salt/etc/VRTScps/db/current:$ cat /etc/vxcps.conf<br />
cps_name=salt<br />
vip=[10.x.x.x] # update x.x.x to your VIP<br />
port=14250<br />
security=0<br />
db=/etc/VRTScps/db<br />
` 
  
<!--more-->


  
\# then start CPS
  
`<br />
/opt/VRTScps/bin/vxcpserv<br />
` 

\# check CPS
  
netstat -anpt |grep 14250
  
tcp 0 0 127.0.0.1:14250 0.0.0.0:* LISTEN 26041/vxcpserv
  
tcp 0 0 10.x.x.x:14250 0.0.0.0:* LISTEN 26041/vxcpserv 

=== Part 2, Setup Password less from Cluster node to CPS server ===
  
When client want to talk/reg the CPS server. they need ssh passwordless from client to CPS server. so this need to be setup before Part 3.

=== Part 3, Configure Cluster node to use CPS server ===
  
root@beihdp01a ~]# /opt/VRTS/install/installvcs -fencing

Veritas Cluster Server 5.1 SP1 Install Program 

Copyright (c) 2010 Symantec Corporation. All rights reserved. Symantec, the Symantec Logo are trademarks or registered trademarks of Symantec Corporation or its affiliates
  
in the U.S. and other countries. Other names may be trademarks of their respective owners.

The Licensed Software and Documentation are deemed to be &#8220;commercial computer software&#8221; and &#8220;commercial computer software documentation&#8221; as defined in FAR Sections 12.212
  
and DFARS Section 227.7202.

Logs are being written to /var/tmp/installvcs-201312040324pwh while installvcs is in progress.

Checking communication on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Checking release compatibility on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Checking VCS installation on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. 5.1.132.000

Veritas Cluster Server 5.1 SP1 Configure Program 

Cluster information verification:

Cluster Name: beihdp

Cluster ID Number: 10

Systems: beihdp01a beihdp01b beihdp01c
  
Would you like to configure I/O fencing on the cluster? [y,n,q] y
      
Checking communication on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Checking release compatibility on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Checking VCS installation on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. 5.1.132.000
      
Checking communication on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Checking release compatibility on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Checking VCS installation on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. 5.1.132.000
      
Checking communication on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Checking release compatibility on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Checking VCS installation on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. 5.1.132.000

Veritas Cluster Server 5.1 SP1 Configure Program 

Fencing configuration
       
1) Configure CP client based fencing
       
2) Configure disk based fencing
       
3) Configure fencing in disabled mode

Select the fencing mechanism to be configured in this Application Cluster: [1-3,q] 1

Does your storage environment support SCSI3 PR? \[y,n,q\] (y) n

In virtualized environments that do not support SCSI-3 PR, VCS attempts to minimize the chances of data corruption with discreet use of timings in the event of unreachable
  
nodes or network partition. However, if a server becomes unresponsive, VCS assumes that the node has left the cluster and reconfigures itself.

This feature only works with UseFence Cluster attribute set to SCSI3 and all coordination points being CP servers

In this environment, either Non-SCSI3 fencing can be configured or fencing can be configured in disabled mode

Do you want to configure Non-SCSI3 fencing? \[y,n,q\] (y) 

Enter the total number of co-ordination points. All co-ordination points should be CP servers: \[b\] (3) 1

Warning: Symantec recommends at least three or more odd number of coordination points to avoid a single point of failure. However, if fencing is configured to use a single
  
CP server, it is strongly recommended to make the CP server highly available by configuring it on a SFHA cluster. It is important to note that during a failover of the CP
  
server in the SFHA cluster, if there is a network partition on the client cluster at the same time, the whole client cluster will be brought down because arbitration
  
facility will not be available for the duration of the failover.

Press [Enter] to continue: 

Veritas Cluster Server 5.1 SP1 Configure Program 

You are now going to be asked for the Virtual IP addresses/hostnames of the CP Servers. Note that the installer assumes these values to be the identical as viewed from all
  
the client cluster nodes.

Press [Enter] to continue:
  
Enter the Virtual IP address/fully qualified host name for the Co-ordination Point Server #1: [b] 10.x.x.x
  
Enter the port in the range \[49152, 65535] which the Co-ordination Point Server 10.240.3.41 would be listening on or simply accept the default port suggested: [b\] (14250) 

Veritas Cluster Server 5.1 SP1 Configure Program 

CPS based fencing configuration: Coordination points verification

Total number of coordination points being used: 1
 	  
CP Server (Port):
 		  
1. 10.240.3.41 (14250)

Is this information correct? \[y,n,q\] (y) 

Veritas Cluster Server 5.1 SP1 Configure Program 

While it is recommended to have secure communication configured between CP Servers and CP client cluster, the client cluster must be in the same mode (secure or non-secure)
  
as the CP servers are.

Since the CP servers are configured in non-secure mode, the installer will not try to configure the client cluster as a secure cluster.

Press [Enter] to continue: 

Veritas Cluster Server 5.1 SP1 Configure Program 

CPS based fencing configuration: Client cluster verification

CPS Admin utility : /opt/VRTScps/bin/cpsadm
 	  
Cluster ID: 10
 	  
Cluster Name: beihdp
 	  
UUID for the above cluster: {58f57018-1dd2-11b2-bf24-8d7f951ee738}

Is this information correct? \[y,n,q\] (y) 

Veritas Cluster Server 5.1 SP1 Configure Program 

Updating client cluster information on CP Server 10.x.x.x
      
Adding the client cluster to the CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done

Registering client node beihdp01a with CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding CPClient user for communicating to CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding cluster beihdp to the CPClient user on CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done

Registering client node beihdp01b with CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding CPClient user for communicating to CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding cluster beihdp to the CPClient user on CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done

Registering client node beihdp01c with CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding CPClient user for communicating to CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;. Done
      
Adding cluster beihdp to the CPClient user on CP Server 10.x.x.x &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
  
Do you want to configure CP Agent on the client cluster? \[y,n,q\] (y)
  
There is already at least one group with a resource of type &#8216;CoordPoint&#8217; as displayed below. Manually check if it has all the attributes set correctly.
  
#Resource Attribute System Value
  
coordpoint Group global vxfen

Press [Enter] to continue: 

Stopping VCS on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Stopping VCS on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Stopping VCS on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done

Updating /etc/vxfenmode file on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/vxenviron file on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/sysconfig/vxfen file on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/llttab file on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done

Updating /etc/vxfenmode file on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/vxenviron file on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/sysconfig/vxfen file on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/llttab file on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done

Updating /etc/vxfenmode file on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/vxenviron file on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/sysconfig/vxfen file on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating /etc/llttab file on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done

Starting Fencing on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Starting Fencing on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Starting Fencing on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Updating main.cf with fencing &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.. Done
      
Starting VCS on beihdp01a &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Starting VCS on beihdp01b &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
Starting VCS on beihdp01c &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
      
I/O Fencing configuration &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230; Done
  
I/O Fencing configuration completed successfully

installvcs log files, summary file, and response file are saved at:

/opt/VRTS/install/logs/installvcs-201312040324pwh

[root@beihdp01a ~]# hastatus -sum

&#8212; SYSTEM STATE
  
&#8212; System State Frozen 

A beihdp01a RUNNING 0
  
A beihdp01b RUNNING 0
  
A beihdp01c RUNNING 0 

&#8212; GROUP STATE
  
&#8212; Group System Probed AutoDisabled State 

B sg_BJHDP01 beihdp01a Y N OFFLINE
  
B sg_BJHDP01 beihdp01b Y N OFFLINE
  
B sg_BJHDP01 beihdp01c Y N OFFLINE
  
B sg_BJTST01 beihdp01a Y N OFFLINE
  
B sg_BJTST01 beihdp01b Y N OFFLINE
  
B sg_BJTST01 beihdp01c Y N OFFLINE
  
B vxfen beihdp01a Y N OFFLINE
  
B vxfen beihdp01b Y N OFFLINE
  
B vxfen beihdp01c Y N OFFLINE 

[root@beihdp01b ~]# cpsadm -s salt -a list_nodes

ClusterName UUID Hostname(Node ID) Registered
  
=========== =================================== ================ ===========
  
beihdp {58f57018-1dd2-11b2-bf24-8d7f951ee738} beihdp01a(0) 0
  
beihdp {58f57018-1dd2-11b2-bf24-8d7f951ee738} beihdp01b(1) 0
  
beihdp {58f57018-1dd2-11b2-bf24-8d7f951ee738} beihdp01c(2) 0 

[root@beihdp01b ~]# tail -f /var/VRTSvcs/log/vxfen/vxfen.log
  
Wed Dec 4 03:06:49 GMT 2013 starting /sbin/vxfen-shutdown
  
Wed Dec 4 03:06:49 GMT 2013 starting retry loop
  
Wed Dec 4 03:06:49 GMT 2013 count is 0
  
Wed Dec 4 03:06:51 GMT 2013 vxfenconfig -U returned 0
  
Wed Dec 4 03:06:51 GMT 2013 exiting normally
  
Wed Dec 4 03:06:51 GMT 2013 /sbin/vxfen-shutdown returned with 0
  
Wed Dec 4 03:06:51 GMT 2013 stopping vxfen.. Done
  
Wed Dec 4 03:06:56 GMT 2013 calling mod_unload.
  
Wed Dec 4 03:25:57 GMT 2013 Invoked vxfen. Starting
  
Wed Dec 4 03:25:57 GMT 2013 starting vxfen..
  
Wed Dec 4 03:26:50 GMT 2013 calling start_fun.
  
Wed Dec 4 03:26:50 GMT 2013 found vxfenmode file
  
Wed Dec 4 03:26:50 GMT 2013 calling /sbin/vxfen-startup in bg
  
Wed Dec 4 03:26:50 GMT 2013 starting vxfen.. Done
  
Wed Dec 4 03:26:51 GMT 2013 starting in vxfen-startup
  
Wed Dec 4 03:26:51 GMT 2013 case -m :: fencing mechanism cps
  
Wed Dec 4 03:26:51 GMT 2013 executing local_info.sh: begin
  
Wed Dec 4 03:26:53 GMT 2013 output was security=0
  
single_cp=1
  
[10.240.3.41]:14250 {57c23368-1dd2-11b2-bbe6-8fe76b5f507b}
  
Wed Dec 4 03:26:53 GMT 2013 executing local_info.sh: end
  
Wed Dec 4 03:26:53 GMT 2013 calling regular vxfenconfig
  
Wed Dec 4 03:27:17 GMT 2013 return value from above operation is 0
  
Wed Dec 4 03:27:17 GMT 2013 output was Log Buffer: 0xffffffff88e082c0

VXFEN vxfenconfig NOTICE Driver will use customized fencing &#8211; mechanism cps
  
Wed Dec 4 03:27:17 GMT 2013 done with script.

\# Issue 1.
  
Wed Dec 4 02:24:57 GMT 2013 output was VXFEN vxfenconfig ERROR V-11-2-1043 Detected a preexisting split brain. Unable to join cluster.
  
Log Buffer: 0xffffffff88d292c0

\# clean the sqlite db (/etc/VRTScps/db/current/cps_db) from CPS server or you can clean up the record for your new Cluster. then let the installvcs -fencing script moving forward.

\# show cluster info from CP server
  
$cd /etc/VRTScps/db/current
  
$sqlite cps_db
  
sqlite> .tables
  
clusters nodes nodesspv user_cluster users
  
sqlite> select * from nodes;
  
0,{58f57018-1dd2-11b2-bf24-8d7f951ee738},1,beihdp01a
  
1,{58f57018-1dd2-11b2-bf24-8d7f951ee738},0,beihdp01b
  
2,{58f57018-1dd2-11b2-bf24-8d7f951ee738},1,beihdp01c
  
sqlite> select * from clusters;
  
{58f57018-1dd2-11b2-bf24-8d7f951ee738},beihdp

\# Issue 2, Even the coordpoint online. the SG still doesn&#8217;t get online
  
Solution:
  
Add Phantom to vxfen SG. 

vxfen beihdp01a ONLINE
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-
  
vxfen beihdp01c ONLINE
                  
coordpoint beihdp01a ONLINE
                  
coordpoint beihdp01c ONLINE
                  
phantom beihdp01a ONLINE
                  
phantom beihdp01c ONLINE 

\# Refer
  
http://www.symantec.com/business/support/index?page=content&id=HOWTO41888