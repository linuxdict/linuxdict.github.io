---
id: 71
title: Linux上配置DNS服务器（来自网络）
date: 2007-10-07T10:42:19+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=141
permalink: '/2007-10-linux%e4%b8%8a%e9%85%8d%e7%bd%aedns%e6%9c%8d%e5%8a%a1%e5%99%a8%ef%bc%88%e6%9d%a5%e8%87%aa%e7%bd%91%e7%bb%9c%ef%bc%89/'
bttc_cache:
  - 1273237340:0
  - 1273237340:0
categories:
  - linux
---
很多朋友学习在Linux上配置DNS服务器的时候，都是参考的在RHEL4或Fedora Core5之前平台上的资料。在Fedora
  
7上，很多东西发生了变化。本文简单介绍一下应对的方法。
  
软件列表

bind-libs-9.4.0-6.fc7
  
bind-chroot-9.4.0-6.fc7
  
bind-utils-9.4.0-6.fc7
  
bind-9.4.0-6.fc7
  
caching-nameserver-9.4.0-6.fc7
  
<!--more-->


  
如果您升级过系统，则软件的版本会略有不同。其中的bind-chroot可以增加DNS服务器的安全，不安装也能工作。

Fedora 7上的bind软件和原来的结构有所不同，没有了以前的/etc/named.conf和 /var/named/chroot/etc/named.conf(前者是后者的符号链接)，导致很多朋友一时不知道该如何配置DNS服务器了，经过简单研究，笔者终结出了DNS服务器的配置方法。

在/var/named/chroot/etc下执行

cat named.caching-nameserver.conf named.rfc1912.zones > named.conf
  
rm named.caching-nameserver.conf named.rfc1912.zones > named.conf
  
[root@maluyao ~]ln -s /var/named/chroot/etc/named.conf /etc/named.conf

上面的步骤是合并named.caching-nameserver.conf named.rfc1912.zones合并到一个文件(/var/named/chrrot/etc/named.conf)中，然后将其删除。实际操作的时候，最好不要删除，而是将这俩个文件移动到其他位置备份。并且为了方便起见，在/etc下作了一个符号链接。

修改named.conf文件，将其中的

view localhost_resolver {
  
match-clients { localhost; };
  
match-destinations { localhost; };
  
recursion yes;
  
};

和

include &#8220;/etc/named.rfc1912.zones&#8221;;

行注释或删除。

Fedora 7中，默认仅仅在回环地址127.0.0.1 和 ::1(IPV6的回环地址)上打开53端口，如果希望在所有地址上都打开53端口，则应该修改named.conf 中

listen-on port 53 { 127.0.0.1; };
  
listen-on-v6 port 53 { ::1; };

为

listen-on port 53 { any; };
  
listen-on-v6 port 53 { any; };

Fedora 7 中的DNS服务器默认只允许127.0.0.1这个客户端(即本机)发起查询，一般我们需要允许所有人查询，这要修改name.conf中的:

allow-query { localhost; };

为

allow-query { any; };

重新启动BIND

/etc/named.conf文件的配置参数说明：

OA 指示该区的权威
  
NS 列出该区的一个名字服务器
  
A 名字到地址的映射
  
PTR 地址到名字的映射
  
CNAME 别名
  
TTL值
  
名字服务器在查询响应中提供这个TTL值，允许其他服务器将数据在缓存中存放TTL所指定的时间。
  
如果你的数据不是经常变动或变动不大，可以考虑将TTL值默认设置为1天。1周大概是这个值的最大限度
  
象1个小时这样短的值也可以使用，但是我们通常不会建议使用短值。
  
SOA记录
  
表示对该区数据而言，这个名字服务器就是最好的信息来源。根据这个SOA记录，我们的名字服务器就享有对区seker.com的权威。每个数据文件都要有SOA记录，每个区数据文件中允许有一个也只允许有一个SOA记录。
  
seker.com. 必须有一个点来结尾。这是因为DNS中有一个简写的惯例，不在seker.com后面加点的话，它就会变成seker.com.seker.com
  
SOA后面每一个名字是seker.com区的主名字服务器的名字。第二个名字就是管理这个区的电子邮件地址
  
（可以把root.改成root@其实这就是一个邮件地址）
  
NS记录
  
我们在每个文件中添加的下一个条目是NS，指定在这个区内我们的权威DNS服务器。

先从 http://www.isc.org/products/BIND/ 下载bind，我下载的是bind-9.3.1rc1.tar.gz

rpm包

bind-chroot-9.2.4-2

bind-libs-9.2.4-2

bind-9.2.4-2

bind-devel-9.2.4-2

bind-utils-9.2.4-16.EL4

caching-nameserver-7.3-3

我下载的文件放在/root目录下
  
进入目录解压缩
  
[root@linux root]#tar xfz bind-9.3.1rc1.tar.gz
  
进如刚解压出来的目录
  
[root@linux root]# cd bind-9.3.1rc1
  
编译配置
  
[root@linux bind-9.3.1rc1]#./configure &#8211;prefix=/usr/local/named &#8211;enable-threads #&#8211;enable-threads开启多线程处理能力
  
[root@linux bind-9.3.1rc1]#make
  
[root@linux bind-9.3.1rc1]#make install
  
进入/usr/local/named 建立etc目录
  
[root@linux bind-9.3.1rc1]#cd /usr/local/named
  
[root@linux named]# mkdir etc
  
生成rndc控制命令的key文件
  
[root@linux named]# sbin/rndc-confgen > etc/rndc.conf
  
从rndc.conf文件中提取named.conf用的key
  
root@linux named]# cd etc
  
[root@linux etc]# tail -10 rndc.conf | head -9 | sed s/#\ //g > named.conf
  
自动在/usr/local/named/etc 生成named,conf文件
  
建立区文件目录
  
[root@linux etc]# mkdir /var/named
  
进入/var/named
  
[root@linux etc]# cd /var/named
  
建立localhost.zone文件
  
[root@linux named]#vi localhost.zone
  
$TTL 86400
  
$ORIGIN localhost.
  
@ 1D IN SOA @ root (
                                          
42 ; serial (d. adams)
                                          
3H ; refresh
                                          
15M ; retry
                                          
1W ; expiry
                                          
1D ) ; minimum

1D IN NS @
                          
1D IN A 127.0.0.1

建立named.local文件
  
[root@linux named]#vi named.local
  
$TTL 86400
  
@ IN SOA localhost. root.localhost. (
                                        
1997022700 ; Serial
                                        
28800 ; Refresh
                                        
14400 ; Retry
                                        
3600000 ; Expire
                                        
86400 ) ; Minimum
                
IN NS localhost.

1 IN PTR localhost.

dig命令直接生成named.root文件
  
[root@linux named]#dig > named.root
  
建立seker.com域名正向解析文件
  
[root@linux named]#vi seker.zone

$ttl 1D
  
@ IN SOA seker.com. root.seker.com. (

1053891162
                                          
3H
                                          
15M
                                          
1W
                                          
1D )

IN NS seker.com.
                          
IN MX 5 seker.com.
  
www IN A 192.168.1.4

建立seker.com域名反向解析文件
  
[root@linux named]#vi seker.local
  
$TTL 86400
  
@ IN SOA seker.com. root.seker.com.(
  
20031001;
  
7200;
  
3600;
  
43200;
  
86400);
  
@ IN NS seker.com.
  
4 IN PTR www.seker.com.

配置named.conf加如以下代码

[root@linux etc]# vi named.conf

options {
  
directory &#8220;/var/named&#8221;; #named区文件目录
  
pid-file &#8220;named.pid&#8221;; #进程id文件名
  
};
  
controls {
          
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
  
};
  
zone &#8220;.&#8221; IN {
          
type hint;
          
file &#8220;named.root&#8221;;
  
};

zone &#8220;localhost&#8221; IN {
          
type master;
          
file &#8220;localhost.zone&#8221;;
          
allow-update { none; };
  
};

zone &#8220;0.0.127.in-addr.arpa&#8221; IN {
          
type master;
          
file &#8220;named.local&#8221;;
          
allow-update { none; };
  
};

zone &#8220;seker.com&#8221; IN {
          
type master;
          
file &#8220;seker.zone&#8221;;
          
allow-update { none; };
  
};

zone &#8220;1.168.192.in-addr.arpa&#8221; IN {
          
type master;
          
file &#8220;seker.local&#8221;;
          
allow-update { none; };
  
};

现在配置完了可以启动BIND了

/usr/local/named/sbin/named -c /usr/local/named/etc/named.conf &

只要显示
  
runing表示运行成功
  
测试DNS
  
[root@linux etc]# host 192.168.1.4
  
4.1.168.192.in-addr.arpa domain name pointer dns.seker.com.
  
如上显示表示DNS反向解析正常
  
[root@linux etc]# ping www.seker.com
  
PING www.seker.com (192.168.1.4) 56(84) bytes of data.
  
如上显示表示正向解析正常
  
DNS配置完成

FAQ：

错误：view.c:347: REQUIRE((&view->references)->refs > 0) failed

rpm –e –nodeps bind-libs-9.2.4-2

yum install bind-libs

service named restart