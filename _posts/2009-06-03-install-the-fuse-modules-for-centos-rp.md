---
id: 335
title: Install the FUSE modules for CentOS
date: 2009-06-03T03:12:20+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=335
permalink: /2009-06-install-the-fuse-modules-for-centos-rp/
bttc_cache:
  - 1273307926:0
  - 1273307926:0
categories:
  - linux
tags:
  - kernel
  - linux
  - tips
---
Install the FUSE modules for CentOS 

rpm -ivh http://download.fedora.redhat.com//pub/epel/5/\`uname -i\`/epel-release-\`cut -d&#8221; &#8221; /etc/redhat-release -f 3 |awk -F&#8221;.&#8221; &#8216;{print $1}&#8217;\`-\`cut -d&#8221; &#8221; /etc/redhat-release -f 3 |awk -F&#8221;.&#8221; &#8216;{print $2}&#8217;\`.noarch.rpm
  
rpm -Uvh http://apt.sw.be/redhat/el5/en/i386/rpmforge/RPMS/rpmforge-release-0.3.6-1.el5.rf.i386.rpm

yum update -y kernel
  
yum install -y kernel-devel
  
yum install -y dkms-fuse.noarch
  
reboot

cd /usr/src/fuse-(some version)/
  
./configure &#8211;with-kernel=/usr/src/kernels/\`uname -r\`*/
  
make && make install

depmod -a
  
modprobe fuse
  
lsmod |grep fuse
  
it should print:
  
fuse 47124 0