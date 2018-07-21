---
id: 687
title: Cygwin telnet tips etc
date: 2011-08-08T20:38:20+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=687
permalink: /2011-08-cygwin-telnet-tips-etc/
categories:
  - Howto
tags:
  - tips
---
Install Telnet Using Cygwin On Windows 7
  
telnet for Cygwin is in inetutils, install the package to gain telnet

Crontab issue:
  
pam_access(crond:account): access denied
  
crond[9985]: CRON (someuser) ERROR: failed to open PAM security session: Success
  
crond[9985]: CRON (someuser) ERROR: cannot set security context

* if has /etc/cron.allow – add users to this file
  
* /etc/security/access.conf – comment out

\# All other users should be denied to get access from all sources.
  
#- : ALL : ALL
  
\# -:ALL EXCEPT root:LOCAL