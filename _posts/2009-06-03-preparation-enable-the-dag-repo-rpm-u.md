---
id: 331
title: 'Preparation  Enable the Dag repo'
date: 2009-06-03T01:08:30+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=331
permalink: /2009-06-preparation-enable-the-dag-repo-rpm-u/
bttc_cache:
  - 1273307926:0
  - 1273307926:0
categories:
  - linux
  - Linux_D
tags:
  - linux
  - server
  - tips
---
Preparation

Enable the Dag repo

rpm -Uhv \
   
http://apt.sw.be/redhat/el5/en/x86\_64/rpmforge/RPMS//rpmforge-release-0.3.6-1.el5.rf.x86\_64.rpm

Enable the Epel repo

rpm -ivh http://download.fedora.redhat.com//pub/epel/5/\`uname -i\`/epel-release-\`cut -d&#8221; &#8221; /etc/redhat-release -f 3 |awk -F&#8221;.&#8221; &#8216;{print $1}&#8217;\`-\`cut -d&#8221; &#8221; /etc/redhat-release -f 3 |awk -F&#8221;.&#8221; &#8216;{print $2}&#8217;\`.noarch.rpm

Install the gcc and other tools

yum install -y make gcc gcc-c++ ncurses-devel.x86\_64 automake autoconf boost-devel.x86\_64 libedit-devel.x86\_64 fuse-devel.x86\_64 rpm-build.x86_64

Get the kernel source from kernel.org

http://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.29.1.tar.bz2

Get the Ceph-0.8 sources package

from: http://ceph.newdream.net/download/

http://ceph.newdream.net/download/ceph-0.8.tar.gz

Proceed

<!--more-->

mkdir build_cluster

cd build_cluster

tar xf linux-2.6.29.1.tar.bz2

tar xf ceph-0.8.tar.gz

cp -r ceph-0.8/src/kernel linux-2.6.29.1/fs/ceph

Edit the linux-2.6.29.1/fs/Kconfig file about line 269

&#8212;-here &#8212;- add the following line &#8212;&#8212;

source &#8220;fs/ceph/Kconfig&#8221;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

it should looks like

(ignore&#8230;.)

source &#8220;net/sunrpc/Kconfig&#8221;
  
source &#8220;fs/smbfs/Kconfig&#8221;
  
source &#8220;fs/ceph/Kconfig&#8221; #add for ceph
  
source &#8220;fs/cifs/Kconfig&#8221;
  
source &#8220;fs/ncpfs/Kconfig&#8221;
  
source &#8220;fs/coda/Kconfig&#8221;

(ignore&#8230;..)

Edit the linux-2.6.29.1/fs/Makefile file and the following line to the end of it.

&#8212;-here &#8212;- add the following line &#8212;&#8212;

obj-$(CONFIG\_CEPH\_FS) &nbsp ; += ceph/

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

make menuconfig

we should find the ceph modules in File Systems-> Network File Systems-> Ceph distributed file system (EXPERIMENTAL)

https://clearspace:8443/clearspace/servlet/JiveServlet/download/1217-1-1138/Picture%2036.png

we are compile a kernel for server, so there are some uneed modules, like sound, wireless, and others

the config we used here is the attachment

make rpm

we will get the new kernel

/usr/src/redhat/RPMS/x86\_64/kernel-2.6.29.1vceph-3.x86\_64.rpm

/usr/src/redhat/SRPMS/kernel-2.6.29.1vceph-3.src.rpm

rpm -ivh /usr/src/redhat/RPMS/x86\_64/kernel-2.6.29.1vceph-3.x86\_64.rpm

Next we need to generate the initrd for modules.

mkinitrd &#8211;without-dmraid /boot/initrd-2.6.29.1vceph 2.6.29.1vceph

edit the /etc/grub.conf add the following lines

&#8212;-here &#8212;- add the following line &#8212;&#8212;

title 2.6.29.1-Vcluster
      
root (hd0,0)
      
kernel /vmlinuz-2.6.29.1vceph ro root=/dev/VolGroup00/LogVol00
      
initrd /initrd-2.6.29.1vceph
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

my /etc/grub.conf looks like

&#8212;-here &#8212;- Start &#8212;&#8212;-

default=1
  
timeout=5
  
splashimage=(hd0,0)/grub/splash.xpm.gz
  
hiddenmenu
  
title CentOS (2.6.25)
      
root (hd0,0)
      
kernel /vmlinuz-2.6.25 ro root=/dev/VolGroup00/LogVol00
      
initrd /initrd-2.6.25.img
  
title 2.6.29.1-Vcluster
      
root (hd0,0)
      
kernel /vmlinuz-2.6.29.1vceph ro root=/dev/VolGroup00/LogVol00
      
initrd /initrd-2.6.29.1vceph

&#8212;-here &#8212;- End &#8212;&#8212;&#8211;

reboot

uname -a
  
Linux cluster01 2.6.29.1vceph #3 SMP Tue Jun 2 17:59:22 CST 2009 x86\_64 x86\_64 x86_64 GNU/Linux

[root@cluster01 cluster]# modprobe ceph

[root@cluster01 cluster]# lsmod |grep ceph
  
ceph &nbs p; 327920 0