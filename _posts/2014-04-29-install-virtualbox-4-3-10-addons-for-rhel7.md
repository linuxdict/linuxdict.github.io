---
id: 841
title: Install Virtualbox 4.3.10 Addons for RHEL7
date: 2014-04-29T00:57:10+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=841
permalink: /2014-04-install-virtualbox-4-3-10-addons-for-rhel7/
categories:
  - Howto
---
When trying to play new Redhat release, RHEL7 as my working desktop.
  
You may hit following error when you install Virtualbox addons 

`<br />
/tmp/vbox.0/r0drv/linux/memobj-r0drv-linux.c: In function ‘rtR0MemObjNativeMapUser’:<br />
/tmp/vbox.0/r0drv/linux/memobj-r0drv-linux.c:1542:26: error: ‘struct mm_struct’ has no member named ‘numa_next_reset’<br />
                 pTask->mm->numa_next_reset = jiffies + 0x7fffffffffffffffUL;<br />
                          ^<br />
make[2]: *** [/tmp/vbox.0/r0drv/linux/memobj-r0drv-linux.o] Error 1<br />
make[1]: *** [_module_/tmp/vbox.0] Error 2<br />
make: *** [vboxguest] Error 2<br />
` 

you need update memobj-r0drv-linux.c,
  
tips: you can quick cp /tmp/vbox.0 out when it decompress completed. then copy the new file in.
  
Ref: https://www.virtualbox.org/ticket/12638