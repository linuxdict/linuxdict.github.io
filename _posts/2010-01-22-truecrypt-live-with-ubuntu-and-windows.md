---
id: 489
title: Truecrypt live with Ubuntu and windows
date: 2010-01-22T18:45:13+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=489
permalink: /2010-01-truecrypt-live-with-ubuntu-and-windows/
bttc_cache:
  - 1273362106:0
  - 1273362106:0
categories:
  - Howto
---
Now the enviorment:

Windows already installed and Truecrypt encrypt the whole disk. and install Ubuntu and keep Windows.

After Ubuntu installed, the Windows disappear.

Reason/Solution: Windows is encrypted with Truecrypt, so Ubuntu can&#8217;t detect the system and generate the dual-boot menu.

so we need to use &#8220;Truecrypt Rescue CD&#8221;, insert it into the computer and restart it. Then it will show: &#8220;&#8230;Install hiding operating system&#8221;

choose &#8220;No&#8221;, then it will ask your password, input your password and then go to Windows now. default it will boot into Ubuntu.

after boot into Windows. “permanently decrypt&#8221; &#8230;.then grub-install /dev/sda

we got dual-boot menu. if any better idea to keep Truecrypt with Windows. share your idea. Thanks.