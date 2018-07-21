---
id: 218
title: Linux-Vserver安装笔记
date: 2009-02-17T21:44:26+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=218
permalink: '/2009-02-linux-vserver%e5%ae%89%e8%a3%85%e7%ac%94%e8%ae%b0/'
bttc_cache:
  - 1273307928:0
  - 1273307928:0
categories:
  - linux
tags:
  - server
---
http://linux-vserver.org/ 官方网站
  
具体不同系统的安装方法：
  
http://linux-vserver.org/Documentation

这里我在CentOS 5.1上安装
  
http://linux-vserver.org/Installation\_on\_CentOS

过程：
  
1、vi /etc/yum.repos.d/dhozac-vserver.repo
  
内容
  
<!--more-->


  
[dhozac-vserver]
  
name=Linux-VServer related packages for CentOS $releasever &#8211; $basearch
  
baseurl=http://rpm.hozac.com/dhozac/centos/$releasever/vserver/$basearch
  
gpgkey=http://rpm.hozac.com/conf/keys/RPM-DHOZAC-GPG-KEY
  
2、yum update yum 更新yum
  
3、yum install kernel 重启系统
  
4、安装Vserver工具
  
yum install util-vserver{,-core,-lib,-sysv,-build}
  
5、/etc/init.d/vprocunhide start
  
6、安装GuestOS（斜体字是可变内容）
  
当然了，如果你知道快的源，可以自己更改一下源
  
/usr/lib/util-vserver/distributions/centos5/yum.repos.d/CentOS-Base.repo
  
命令创建虚拟主机
  
vserver _enlampv1_ build -m yum &#8211;context _42_
      
&#8211;hostname _enlampv1.enlamp.cn_
      
&#8211;interface eth0:_192.168.1.11/24_ &#8212; -d centos5
  
7、安装yum
  
vyum enlampv1 &#8212; install yum
  
vserver enlampv1 pkgmgmt internalize
  
8、启动虚拟机
  
vserver enlampv1 start
  
vserver enlampv1 enter 进入系统
  
没有vi，呵呵，echo修改各个文件了。像/etc/reslove.conf等文件。