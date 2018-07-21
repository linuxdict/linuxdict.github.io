---
id: 506
title: Resolve and Caching with Bind9 Nameserver
date: 2010-03-18T01:52:36+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=506
permalink: /2010-03-resolve-and-caching-with-bind9-nameserver/
bttc_cache:
  - 1273362105:0
  - 1273362105:0
categories:
  - Howto
---
Needs:
  
We are required to resolve our internal domains on a local nameserver and external (Internet) domains from ISP&#8217;s nameserver. There are different solutions to this problem, but in this howto, we are going to solve it through configuring a combination of caching-nameserver and BIND 9.

Installation:
  
$yum install caching-nameserver bind*
  
<!--more-->


  
Configuration:
  
Step1. check /etc/named.caching-nameserver.conf , if exist, plz go on
  
`include "/etc/named.rfc1912.zones";`

Step2. add our zones (bold lines) to /etc/named.rfc1912.zones, it should like:
  
`<br />
......<br />
zone "0.in-addr.arpa" IN {<br />
        type master;<br />
        file "named.zero";<br />
        allow-update { none; };<br />
};<br />
<strong>zone "linuxdict.com" IN {<br />
        type master;<br />
        file "linuxdict.com.zone";<br />
        allow-update { none; };<br />
};</strong>`

Step3. create our zone file in /var/named/chroot/var/named/ (if doesn&#8217;t exist, creat in /var/named)
  
/var/named/chroot/var/named/linuxdict.com.zone, content of our zone file
  
`$TTL    86400<br />
@               IN SOA  @ xfsuper.gmail.com. (<br />
                                        2010031803             ; serial (d. adams)<br />
                                        3H              ; refresh<br />
                                        15M             ; retry<br />
                                        1W              ; expiry<br />
                                        1D )            ; minimum<br />
@               IN NS           ns.linuxdict.com.<br />
winxp           IN A            192.168.1.107<br />
ns              IN A            192.168.1.201<br />
dev             IN CNAME        ns<br />
monitor         IN A            192.168.1.202<br />
repo            IN A            192.168.1.203<br />
` 

Step4. service named start 

Step5. change client DNS 🙂 

PS: don&#8217;t forget to change the options:
  
`listen-on port 53 { 127.0.0.1;your_dns_server_ip; };<br />
allow-query     { 192.168.1.0/24; };<br />
allow-query-cache { localhost; 192.168.1.0/24;};`