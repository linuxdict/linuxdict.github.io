---
id: 524
title: Change vdi UUID with VBoxManage
date: 2010-04-02T17:17:07+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=524
permalink: /2010-04-change-vdi-uuid-with-vboxmanage/
bttc_cache:
  - 1273363923:0
  - 1273363923:0
categories:
  - Howto
tags:
  - tips
  - virtualbox
---
We can directly copy the vdi for new VirtualBox vms.but the UUID will be the same as old one. so we need to change the UUID

$VBoxManage internalcommands setvdiuuid /opt/vms/c52_master.vdi
  
VirtualBox Command Line Management Interface Version 3.0.10
  
(C) 2005-2009 Sun Microsystems, Inc.
  
All rights reserved.
  
UUID changed to: aa742648-c3f4-408f-bde8-827dadff5cca

if in Windows, find the installation directory of Virtualbox and then run the VBoxManager.exe command in cmd lines.