---
id: 750
title: Rundeck, operate batch hosts at the same time
date: 2012-08-23T19:12:07+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=750
permalink: /2012-08-rundeck-operate-batch-hosts-at-the-same-time/
categories:
  - Howto
  - Linux_D
tags:
  - tools
---
<a title="RunDeck" href="http://rundeck.org" target="_blank">Rundeck</a>, a web-accessible console for dispatching commands and scripts to your nodes. Dispatch shell commands and scripts across all your physical or virtual nodes from a web-based or command-line interface. Automate ad-hoc and routine procedures. Use the API and plugins to integrate with other services. Use your LDAP/AD for authentication, and configure extensive access control.

Install Steps:

rpm -Uvh http://rundeck.org/latest.rpm
  
yum install rundesk
  
/etc/init.d/rundeckd start
  
http://your_host:4440
  
Default account: admin/admin