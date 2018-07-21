---
id: 526
title: Build HA cluster with keepalived
date: 2010-04-02T19:39:40+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=526
permalink: /2010-04-build-ha-cluster-with-keepalived/
bttc_cache:
  - 1273363923:0
  - 1273363923:0
categories:
  - Howto
---
OS: CentOS 5.4
  
Software:
  
keepalived, openssl097a, lighttpd
  
Arch:
  
&#8212;&#8212;&#8212;&#8212;&#8212;|–lb_master (192.168.1.101/24)
  
Visitors -(VIP) -|
  
&#8212;&#8212;&#8212;&#8212;&#8212;|–lb_slave (192.168.1.102/24)
  
VIP: 192.168.1.100/24

**Install**
  
<!--more-->


  
0. preparation: [enable Two important repo](http://192.168.1.77:8880/2009-06-enable-two-important-repo-for-centos-5/) 
  
1. wget ftp://rpmfind.net/linux/dag/redhat/el4/en/i386/dag/RPMS/keepalived-1.1.13-5.el4.rf.i386.rpm
  
\# keepalived need old libs libssl.so.4 and libcrypto.so.4,if you use some other OS, maybe no need.
  
2. yum install -y openssl097a lighttpd
  
3. rpm -ivh keepalived-1.1.13-5.el4.rf.i386.rpm
  
4. /etc/init.d/keepalived && chkconfig keepalived on && /etc/init.d/lighttpd && chkconfig lighttpd on
  
5. check with command $ip addr show eth0
  
\# if the above steps, no error. let&#8217;s configure the keepalived.

**Configuration**
  
$mv /etc/keepalived/keepalived.conf /etc/keepalived/keepalived.conf.back
  
$touch /etc/keepalived/keepalived.conf
  
#edit /etc/keepalived/keepalived.conf
  
\# Master contents:
  
&#8212;begin&#8212;&#8212;content cut here&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;
  
vrrp\_script chk\_http_port {
  
script &#8220;/usr/bin/killall -0 lighttpd&#8221;
  
interval 2
  
weight 2
  
}

vrrp\_instance VI\_1 {
  
state MASTER
  
interface eth0
  
virtual\_router\_id 51
  
 **priority 101**
  
advert_int 1
  
authentication {
  
auth_type PASS
  
auth_pass 1111
  
}
  
virtual_ipaddress {
  
192.168.1.100/24 dev eth0
  
}
  
}

&#8212;end&#8212;&#8212;content cut here&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

\# Slave contents:
  
&#8212;begin&#8212;&#8212;content cut here&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;
  
vrrp\_script chk\_http_port {
  
script &#8220;/usr/bin/killall -0 lighttpd&#8221;
  
interval 2
  
weight 2
  
}

vrrp\_instance VI\_1 {
  
state MASTER
  
interface eth0
  
virtual\_router\_id 51
  
 **priority 100**
  
advert_int 1
  
authentication {
  
auth_type PASS
  
auth_pass 1111
  
}
  
virtual_ipaddress {
  
192.168.1.100/24 dev eth0
  
}
  
}

&#8212;end&#8212;&#8212;content cut here&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

$/etc/init.d/keepalived restart
  
$tail -f /var/log/messages
  
&#8230;&#8230;&#8230;.
  
Apr 3 11:34:15 stage Keepalived\_vrrp: VRRP\_Instance(VI_1) Sending gratuitous ARPs on eth0 for 192.168.1.100
  
Apr 3 11:34:15 stage Keepalived_vrrp: Netlink reflector reports IP 192.168.1.100 added
  
Apr 3 11:34:15 stage Keepalived_healthcheckers: Netlink reflector reports IP 192.168.1.100 added
  
Apr 3 11:34:20 stage Keepalived\_vrrp: VRRP\_Instance(VI_1) Sending gratuitous ARPs on eth0 for 192.168.1.100
  
&#8230;&#8230;&#8230;

Test
  
#edit the /srv/www/lighttpd/index.htm
  
#master
  
$echo &#8220;I am master&#8221; > /srv/www/lighttpd/index.htm
  
#slave
  
$echo &#8220;I am slave&#8221; > /srv/www/lighttpd/index.htm
  
\# shutdown master
  
$curl 192.168.1.100
  
I am slave
  
\# start master
  
$curl 192.168.1.100
  
I am master
  
\# some info from messages when master is down
  
Apr 3 11:36:24 stage Keepalived\_vrrp: VRRP\_Instance(VI_1) Entering BACKUP STATE
  
Apr 3 11:36:24 stage Keepalived\_vrrp: VRRP\_Instance(VI_1) removing protocol VIPs.
  
Apr 3 11:36:24 stage Keepalived_vrrp: Netlink reflector reports IP 192.168.1.100 removed
  
Apr 3 11:36:24 stage Keepalived_healthcheckers: Netlink reflector reports IP 192.168.1.100 removed

Extend
  
RTFM, the keepalived is very complex and good, it has lots of options, this is only one simple tutorial.