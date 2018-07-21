---
id: 510
title: Install and set up Adobe Flex SDK on linux
date: 2010-03-25T00:19:24+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=510
permalink: /2010-03-install-and-set-up-adobe-flex-sdk-on-linux/
bttc_cache:
  - 1273362104:0
  - 1273362104:0
categories:
  - Howto
  - linux
---
1. Install JDK

2. Download Adobe Flex SDK (Free Adobe Flex SDK)
  
http://opensource.adobe.com/wiki/display/flexsdk/Downloads

3. if run as root, you can create directory in /opt/flexsdk or other places
  
cd /opt/flexsdk
  
unzip ~/flex\_sdk\_4.0.0.14159.zip
  
if work as normal user
  
mkdir ~/flexsdk
  
cd ~/flexsdk
  
unzip ~/flex\_sdk\_4.0.0.14159.zip

4. change the variables
  
vi ~/.bashrc
  
#add the following lines
  
export PATH=$PATH:/opt/flexsdk/bin:~/flexsdk/bin
  
. ~/.bashrc

5. Test
  
$mxmlc &#8211;help
  
Adobe Flex Compiler (mxmlc)
  
Version 4.0.0 build 14159
  
Copyright (c) 2004-2009 Adobe Systems, Inc. All rights reserved.