---
id: 319
title: Besides the Mongrel_Rail for RoR app
date: 2009-05-13T03:14:06+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=319
permalink: /2009-05-besides-the-mongrel_rail-for-ror-app-i/
bttc_cache:
  - 1273330855:0
  - 1273330855:0
categories:
  - Linux_D
tags:
  - linux
  - ruby
  - server
---
Besides the Mongrel_Rail for RoR app, I found a new server modules:
  
Phusion Passenger
  
It is easy to deploy with Apache
  
http://www.modrails.com/

I have tried it, it works well, maybe more test on it in the future.

my ruby.conf for my app in Apache

&#8220;<"VirtualHost *:80">&#8221;
	  
ServerName myip
	  
DocumentRoot /path/to/app/public/ # the RoR app&#8217;s public directory

AddOutputFilterByType DEFLATE text/html text/plain text/xml application/xml application/xhtml+xml text/javascript text/css application/x-javascript
	  
BrowserMatch ^Mozilla/4 gzip-only-text/html
	  
BrowserMatch ^Mozilla/4.0[678] no-gzip
	  
BrowserMatch bMSIE !no-gzip !gzip-only-text/html

ExpiresActive On
	  
ExpiresByType image/gif A2592000
	  
ExpiresByType application/x-javascript A2592000
	  
ExpiresByType text/css A2592000
	  
ExpiresByType text/html M604800
  
&#8220;<"/VirtualHost">&#8220;