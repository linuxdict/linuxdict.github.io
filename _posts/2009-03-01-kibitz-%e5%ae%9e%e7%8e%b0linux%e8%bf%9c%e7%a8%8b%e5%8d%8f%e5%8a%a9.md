---
id: 248
title: 'kibitz&#8211;实现Linux远程协助'
date: 2009-03-01T21:27:14+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=248
permalink: '/2009-03-kibitz-%e5%ae%9e%e7%8e%b0linux%e8%bf%9c%e7%a8%8b%e5%8d%8f%e5%8a%a9/'
bttc_cache:
  - 1273307927:0
  - 1273307927:0
categories:
  - linux
---
在Linux下，有一个基于expect的工具:kibitz可以实现两个登陆用户(可以是同一个用户，例如root但是通过不同的终端登陆的)。kibitz是expect里面一个包，所以首先要保证linux安装expect。

一、检查系统是否安装有expect

[username@localhost:~]$ rpm -qa | grep expect
  
expect-5.43.0-5.1

二、检查是否有kibitz命令

[username@localhost:~]$ whereis kibitz
  
kibitz: /usr/bin/kibitz /usr/share/man/man1/kibitz.1.gz
  
<!--more-->


  
三、查看当前登陆的2个用户

[username@localhost:~]$ w
   
21:22:28 up 6:04, 2 users, load average: 0.89, 0.55, 0.23
  
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
  
edy pts/0 192.168.188.8 13:15 0.00s 0.16s 0.00s w
  
edy pts/1 222.\*.\*.53 21:15 3:12 0.07s 0.07s -bash

可以看到2个登陆终端为 pts/0，另外一方为 pts/1

四、发起方运行：

[username@localhost:~]$ kibitz -tty pts/1 username

asking root to type: kibitz -4517

在被邀请一方的终端上会出现以下提示：

[username@localhost:~]$
  
Message from username@www.enlamp.cn on pts/0 at 21:17 &#8230;
  
Can we talk? Run: kibitz -9315
  
EOF

此时在被邀请方复制 kibitz -9315在 EOF 后面，回车

五、这样，就完成了共享同一个登陆shell的步骤，试着在一个终端下输入命令，可以看到另外一个终端显示一样的输出，而且是实时的，互相都能控制，