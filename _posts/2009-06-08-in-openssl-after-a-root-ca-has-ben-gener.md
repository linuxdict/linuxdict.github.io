---
id: 343
title: Use Openssl to create a root CA
date: 2009-06-08T00:34:14+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=343
permalink: /2009-06-in-openssl-after-a-root-ca-has-ben-gener/
bttc_cache:
  - 1273332161:0
  - 1273332161:0
categories:
  - linux
tags:
  - linux
  - security
  - tips
---
In Openssl after a root CA has ben generated here are the following commands to create an intermediate CA;

as root

/etc/pki/tls/misc/CA –newca

/etc/pki/tls/misc/CA -newreq

some Generic Certificate Authority (usually a server)
  
Enter Enter

/etc/pki/tls/misc/CA –signCA
  
PassPhrase: Demo

newreq.pem is key with CSR request inside
  
newcert.pem is certificate
  
new\_to\_open_ssl is offline 

How to Create Self-Signed SSL Certificates with OpenSSL
  
http://www.xenocafe.com/tutorials/linux/centos/openssl/self\_signed\_certificates/index.php