---
id: 748
title: 'Sendmail issue: Relaying denied'
date: 2012-08-10T22:13:34+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=748
permalink: /2012-08-sendmail-issue-relaying-denied/
categories:
  - solaris
---
Aug 11 05:55:40 relay\_host sendmail[25741]: [ID 801593 mail.notice] q7B4teTq025741: ruleset=check\_rcpt, arg1=<my\_no\_spam\_account@gmail.com>, relay=you\_host_name1.com \[10.23.4.224\] (may be forged), reject=550 5.7.1 <xfsuper@gmail.com>&#8230; Relaying denied. IP name possibly forged [10.23.4.224]
  
Aug 11 05:55:40 relay_host sendmail[25741]: [ID 801593 mail.info] q7B4teTq025741: from=<root@your\_real\_host\_name.com>, size=1741, class=0, nrcpts=0, proto=ESMTP, daemon=MTA-v4, relay=you\_host_name1.com \[10.23.4.224\] (may be forged)

the Relay host won&#8217;t allow your email goes out. because your hostname is not match with DNS.

nslookup 10.23.4.224 , check the domain. and compare with your real host.