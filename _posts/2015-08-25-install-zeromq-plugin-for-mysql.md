---
id: 889
title: Install ZeroMQ plugin for MySQL
date: 2015-08-25T02:28:24+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=883
permalink: /2015-08-install-zeromq-plugin-for-mysql/
categories:
  - Howto
tags:
  - mysql
---
Following steps in CentOS 6.x

Download cmake , use the binary one. such as: cmake-3.2.3-Linux-x86_64.sh
   
http://www.cmake.org/download/

Install Cmake
   
chmod +x cmake-3.2.3-Linux-x86_64.sh
   
./cmake-3.2.3-Linux-x86_64.sh

Get mysql zeromq plugin:
   
git clone https://github.com/netkiller/mysql-zmq-plugin.git
  
<!--more-->

Update headers:
   
cd mysql-zmq-plugin
   
vi CMakeLists.txt , replace with your own headers
   
&#8221;INCLUDE_DIRECTORIES(/usr/local/mysql-xxx/include)&#8221;
   
&#8221;INCLUDE_DIRECTORIES(/usr/local/zeromq-xxx/include)&#8221;
   
cmake .
   
make
  
Then you will get libzeromq.so
   
sudo cp libzeromq.so /path/to/mysql/plugin

Refer:

http://zeromq.org/event:zeromq-for-mysql

Known issue:
  
If you got following complain:

<pre>/usr/bin/ld: cannot find -lzmq
collect2: ld returned 1 exit status
make[2]: *** [libzeromq.so] Error 1
make[1]: *** [CMakeFiles/zeromq.dir/all] Error 2
</pre>

you can
   
ln -s your\_zmq\_so to /lib64/libzmq.so