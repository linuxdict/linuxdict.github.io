---
id: 497
title: genkey to generate your own certificates
date: 2010-02-27T20:00:16+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=497
permalink: /2010-02-genkey-to-generate-your-own-certificates/
bttc_cache:
  - 1273362105:0
  - 1273362105:0
categories:
  - Howto
---
there are some methods:

1. use openssl such as:
  
openssl genrsa -out /etc/httpd/conf/ssl.key/myserver.net.key 1024
  
openssl req -new -key /etc/httpd/conf/ssl.key/myserver.net.key -out /etc/httpd/conf/ssl.csr/myserver.net.key.csr
  
openssl req -new -key /etc/httpd/conf/ssl.key/myserver.net.key -x509 -out /etc/httpd/conf/ssl.crt/myserver.net.crt -days 999

2. install crypto-utils
  
sudo /usr/bin/genkey linuxdict.com &#8211;days 1024
  
follow the instruction, very simple, isn&#8217;t it ?

Then you can use your own cert for your application such as apache,postfix and so on.