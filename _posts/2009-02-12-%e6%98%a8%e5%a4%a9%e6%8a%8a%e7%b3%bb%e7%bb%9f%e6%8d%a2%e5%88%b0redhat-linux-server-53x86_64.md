---
id: 190
title: 昨天把系统换到Redhat Linux Server 5.3(x86_64)
date: 2009-02-12T15:35:11+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=190
permalink: '/2009-02-%e6%98%a8%e5%a4%a9%e6%8a%8a%e7%b3%bb%e7%bb%9f%e6%8d%a2%e5%88%b0redhat-linux-server-53x86_64/'
bttc_cache:
  - 1273340352:0
  - 1273340352:0
categories:
  - Linux桌面
---
用了好久的Ubuntu做桌面，感觉渐渐熟悉了。想换换口味，虽然服务器一直用CentOS
  
但是桌面因为这样那样的问题没怎么用redhat系列的东西。
  
刚好RHEL5.3刚刚发布，从http://rhn.redhat.com注册了一个帐号。
  
下载了一个DVD，现在一张cd光盘不行了。不知道Centos5.3可不可以。

网络安装的，很快就完成了。
  
下面记录一些过程：<!--more-->

添加本地源：
  
cat /etc/yum.repos.d/rhel-base.repo
  
[base]
  
name=Red Hat Enterprise Linux $releasever &#8211; Base
  
baseurl=http://192.168.90.167/rhel5/Server
  
gpgcheck=1

安装显卡驱动：
  
yum install -y gcc gcc-c++ kernel-devel
  
./NVIDIA-Linux-x86_64-180.22-pkg2.run

yum过程中出现这个错误：
  
warning: rpmts_HdrFromFdno: Header V3 DSA sign
  
解决：
  
rpm &#8211;import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

添加chinese（中文）支持
  
yum install -y &#8220;@Chinese Support&#8221;

Flash插件官方的一开就崩溃
  
解决方法:
  
yum install -y firefox.x86_64
  
http://labs.adobe.com/downloads/flashplayer10.html

Pidgin用源码编译（2.5.4)
  
./configure &#8216;&#8211;prefix=/usr/local/pidgin&#8217; &#8216;&#8211;disable-screensaver&#8217; &#8216;&#8211;disable-gstreamer&#8217;
  
&#8216;&#8211;disable-meanwhile&#8217; &#8216;&#8211;disable-avahi&#8217; &#8216;&#8211;disable-dbus&#8217; &#8216;&#8211;disable-tcl&#8217; &#8216;&#8211;disable-sm&#8217;
  
&#8216;&#8211;disable-startup-notification&#8217; &#8216;&#8211;disable-gtkspell&#8217;