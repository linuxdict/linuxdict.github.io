---
id: 310
title: online site to gen passwords
date: 2009-04-30T02:22:10+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=310
permalink: /2009-04-good-online-site-to-gen-passwords-http/
bttc_cache:
  - 1273332162:0
  - 1273332162:0
categories:
  - Linux_D
tags:
  - security
---
good online site to gen passwords
  
http://www.goodpassword.com

good tools to manage your passwords
  
http://www.clipperz.com/open\_source/clipperz\_community_edition

we can also use the following script:

#!/bin/sh
  
cat /dev/urandom| tr -dc &#8216;0-9a-zA-Z!@#$%^&*_+-&#8216;|head -c 10;echo