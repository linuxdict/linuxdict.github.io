---
id: 700
title: ldap and sudo issue on Linux box
date: 2011-12-19T17:16:36+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=700
permalink: /2011-12-ldap-and-sudo-issue-on-linux-box/
categories:
  - linux
---
issue with sudo, we can login with ldap account but can’t sudo -i. When turned on sudoer debug, got following error.
  
sudo: user_matches=1
  
sudo: host_matches=0
  
sudo: sudo\_ldap\_lookup(0)=0x40
  
[sudo] password for edy:

Actually the same configuration works on other hosts.
  
On broken-host, debug info,
  
sudo: found:cn=UNIX-Team-root,ou=SUDOers,dc=abc,dc=com
  
sudo: ldap sudoUser netgroup &#8216;+unixadms&#8217; &#8230; not
  
<!--more-->


  
On working-host, debug info,
  
sudo: found:cn=UNIX-Team-root,ou=SUDOers,dc=abc,dc=com
  
sudo: ldap sudoUser netgroup &#8216;+unixadms&#8217; &#8230; MATCH!

finally turned out domainname issue.
  
working-host:
  
$ domainname
  
abc.com

broken-host
  
$ domainname
  
(none)
  
Changed domainname using “domainname command”
  
\# domainname abc.com

Then everything works fine.