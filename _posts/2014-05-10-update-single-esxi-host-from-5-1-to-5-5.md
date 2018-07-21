---
id: 844
title: update single esxi host from 5.1 to 5.5
date: 2014-05-10T10:36:44+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=844
permalink: /2014-05-update-single-esxi-host-from-5-1-to-5-5/
categories:
  - Howto
tags:
  - esxi
  - vmware
---
1. download the latest esxi offline bundle.
  
ESXi 5.5 Update 1 Offline Bundle
  
File size: 624 MB File type: zip

2. upload the offline bundle to esxi host with client or scp

3. update the esxi with ssh
  
~ # esxcli software profile update -d /vmfs/volumes/vmdata/iso/update-from-esxi5.5-5.5_update01.zip -p ESXi-5.5.0-20140302001-standard
  
Update Result
     
Message: The update completed successfully, but the system needs to be rebooted for the changes to be effective.
     
Reboot Required: true
     
VIBs Installed: VMware\_bootbank\_ata-pata-amd_0.3.10-3vmw.550.0.0.1331820 &#8230;
     
VIBs Removed: VMware\_bootbank\_ata-pata-amd_0.3.10-3vmw.510.0.0.799733 &#8230;

Btw, -p means profile name. you can get the profile name from offline bundle zip. file. update-from-esxi5.5-5.5_update01.zip->metadata.zip->profiles