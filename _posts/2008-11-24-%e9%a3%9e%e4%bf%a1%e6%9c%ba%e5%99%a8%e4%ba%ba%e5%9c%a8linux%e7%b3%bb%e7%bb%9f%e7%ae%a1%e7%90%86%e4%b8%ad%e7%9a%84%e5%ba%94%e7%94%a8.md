---
id: 103
title: 飞信机器人在linux系统管理中的应用
date: 2008-11-24T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=65
permalink: '/2008-11-%e9%a3%9e%e4%bf%a1%e6%9c%ba%e5%99%a8%e4%ba%ba%e5%9c%a8linux%e7%b3%bb%e7%bb%9f%e7%ae%a1%e7%90%86%e4%b8%ad%e7%9a%84%e5%ba%94%e7%94%a8/'
bttc_cache:
  - 1273132759:0
  - 1273132759:0
categories:
  - LAMP
---
今天逛www.bsdlover.cn 看到一篇关于飞信机器人的文章

飞信机器人官方网站：
  
http://www.it-adv.net/

闲话少叙，开始飞信之旅。<!--more-->

OS: CentOS5 (x86_64)

1 下载
  
http://www.it-adv.net/index.php?action=downloads

wget http://www.it-adv.net/fetion/library32.rar
  
wget http://www.it-adv.net/fetion/download/fetion20080910048-linux.tar.gz

2 添加必须的库
  
解压 unrar e library32.rar /usr/lib/
  
ldconfig -v |grep ACE
  
应该有如下显示：
  
libACE.so.5.4.7 -> libACE.so.5.4.7
  
libACE\_SSL.so.5.4.7 -> libACE\_SSL.so.5.4.7

3 tar xvzf fetion20080910048-linux.tar.gz
  
mv install /usr/local/fetion
  
cd /usr/local/fetion ; ./fetion -u 手机号 -p 密码

安装完成

联合其他脚本
  
目标：我要检测磁盘情况，防止有些磁盘被占满。当然了，quota可以做到。
  
假设我没作quota

我写的脚本

/srv/check_disk.sh
  
#!/bin/bash

#
  
#
  
\# Check the Harddisk usesage and warnings
  
\# Author: xfsuper@gmail.com
  
\# Date: 2008/11/5
  
#

\# Warninglimit is 2G default
  
\# lowlimit is 1G default
  
warninglimit=2000000
  
lowlimit=1000000

filesystems=\`df -h | awk &#8216;{print $1}&#8217; |grep /dev\`

for fs in $filesystems
  
do
  
size=\`df -k $fs |grep $fs |awk &#8216;{ print $4; }&#8217;\`

if [ $size -lt $lowlimit ]; then
  
size=$((size/(1024*1024)))
  
echo &#8220;URGENT: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; >/tmp/disk_check
  
echo &#8220;sms 158XXXX3553 URGENT: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; > /tmp/send_urg
  
echo &#8220;exit&#8221; >> /tmp/send_urg

####### send settings
  
mail -s &#8220;URGENT: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; -c xfsuper@gmail.com xfsuper@gmail.com.com < /tmp/disk_check
  
<span style="font-style:italic;">/usr/local/fetion/fetion -u 158XXXX3553 -b /tmp/send_urg -p XXXXX</span>

break
  
fi
  
if [ $size -lt $warninglimit ]; then
  
size=$((size/(1024*1024)))
  
echo &#8220;Warning: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; > /tmp/disk\_check\_warn
  
echo &#8220;sms 158XXXX3553 Warning: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; > /tmp/send_warn
  
echo &#8220;exit&#8221; >> /tmp/send_warn

mail -s &#8220;Warning: Low disk space for $fs in $HOSTNAME,Now it is $size G only&#8221; -c xfsuper@gmail.com xfsuper@gmail.com.com < /tmp/disk\_check\_warn
  
<span style="font-style:italic;">/usr/local/fetion/fetion -u 158XXXX3553 -b /tmp/send_warn -p XXXXX </span>
  
fi

done