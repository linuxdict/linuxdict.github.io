---
id: 632
title: 'Converting a virtual disk image: VDI to VMDK to a raw loopback file you can mount'
date: 2011-07-07T06:35:43+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=632
permalink: /2011-07-converting-a-virtual-disk-image-vdi-to-vmdk-to-a-raw-loopback-file-you-can-mount/
categories:
  - Howto
tags:
  - tips
  - virtualbox
---
By default, VirtualBox creates virtual disk images in a special format called VDI, which is unique to VirtualBox. Disk images are stored in $HOME/.VirtualBox/HardDisks.

You&#8217;ll need to convert VDI into another format if you want to run a VirtualBox VM on another virtualization platform, such as VMWare or KVM.

The VMDK virtual disk format is a good choice because even though it originated with VMWare it is supported by other virtualization platforms including VirtualBox and KVM.

VirtualBox enables the conversion using the low-level &#8220;VBoxManage clonehd&#8221; command:

VBoxManage list hdds # prints a list of disk image UUIDs
  
VBoxManage clonehd <UUID> -o converted.vmdk format VMDK
  
cd ~/.VirtualBox/HardDisks/
  
ls -la converted.vmdk

Once you have converted to VMDK you can use qemu-img, a tool bundled with qemu (KVM&#8217;s virtualization backend) to further convert VMDK to other formats.

A particularly useful format to convert to is &#8216;raw&#8217; which you can then mount as a loopback device:

apt-get install qemu
  
qemu-img convert -f vmdk converted.vmdk -O raw converted.raw
  
mount -o loop converted.raw /mnt