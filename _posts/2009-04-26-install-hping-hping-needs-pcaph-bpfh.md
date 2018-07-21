---
id: 296
title: 'install hping  hping needs pcap.h'
date: 2009-04-26T07:48:03+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=296
permalink: /2009-04-install-hping-hping-needs-pcaph-bpfh/
bttc_cache:
  - 1273332162:0
  - 1273332162:0
categories:
  - Linux_D
tags:
  - network
  - security
---
install hping
  
hping needs pcap.h, bpf.h, we should install libpcap-devel
  
wget http://www.hping.org/hping3-20051105.tar.gz

there is sth need to change
  
ln -s /usr/include/pcap-bpf.h /usr/include/bpf.h

vi libpcap_stuff.c script.c
  
change the net/bpf.h into bpf.h

./configure && make && make install

but it is easy in FreeBSD
  
cd /usr/ports/net/hping-devel
  
make && make install 

hping has much features to test the network!

http://www.securityfocus.com/infocus/1787
  
http://www.securityfocus.com/infocus/1791