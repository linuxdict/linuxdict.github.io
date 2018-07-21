---
id: 440
title: Web Cookies
date: 2009-07-29T18:41:04+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=440
permalink: /2009-07-web-cookies/
bttc_cache:
  - 1273344708:0
  - 1273344708:0
categories:
  - LAMP
tags:
  - linux
  - Php
  - tips
---
The programmers met a problem when use Typo3, the clients can&#8217;t login with IE but can login with Firefox/Opera.
  
After the investigation , we find the problem is the cookies. Typo3 can set the domain for the cookies. change the setting to &#8220;.domain.com&#8221; it works.

btw, close the browers and clean the cookies the most right way.
  
In order to do this properly, **remember to close your browser first.** This is because all your **cookies are held in memory until you close your browser.** So, if you delete the file with your browser open, it will make a new file when you close it, and your cookies will be back. 

Refer of the cookies.
  
http://www.cookiecentral.com/faq/
  
http://www.howstuffworks.com/cookie.htm
  
http://tools.ietf.org/html/rfc2109
  
http://tools.ietf.org/html/rfc2965