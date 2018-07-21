---
id: 800
title: 'ssh: access denied for user'
date: 2013-06-19T20:36:56+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=800
permalink: /2013-06-ssh-access-denied-for-user/
categories:
  - linux
tags:
  - linux
  - ssh
---
Issue:
  
Jun 20 03:18:04 localhost sshd[512]: Failed password for iamid from 10.x.x.1 port 44241 ssh2
  
Jun 20 03:18:04 localhost sshd[513]: fatal: Access denied for user iamid by PAM account configuration

check /var/log/secure, got above messages.

tips to troubleshooting:

1. /etc/nologin exists or not, if exists, remove it.
  
2. /etc/security/access.conf, whether your group/user exists in allow list.

if still have issue, turn on DEBUG for sshd.