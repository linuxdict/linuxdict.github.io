---
id: 466
title: Another Easy and Free Mail Groupware
date: 2009-12-25T20:51:43+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/2009-12-another-easy-and-free-mail-groupware/
permalink: /2009-12-another-easy-and-free-mail-groupware/
bttc_cache:
  - 1273324672:0
  - 1273324672:0
categories:
  - Linux_D
tags:
  - mail
---
There is Zimbra Groupware for the enterprise. also there is one more choice: Citadel Groupware 

Citadel Groupware is a turnkey open-source solution for email and collaboration. One simple installation delivers a multitude of powerful features, including:

email
  
calendaring/scheduling
  
address books
  
bulletin boards
  
mailing list server
  
instant messaging
  
wiki
  
multiple domain support
  
a powerful web interface

The web server/Mta are all tagged with Cit, of course you can change web server to Apache. it support spam and anti-virus. 

very easy install step on Ubuntu
  
sudo apt-get install clamav clamav-milter spamassassin citadel-suite amavisd-new -y

then goto http://urip/ to test

Official site: http://www.citadel.org/doku.php