---
id: 344
title: 'warning: Certificate validation failed'
date: 2009-06-08T02:56:45+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=344
permalink: /2009-06-warning-certificate-validation-failed/
bttc_cache:
  - 1273311936:0
  - 1273311936:0
categories:
  - linux
tags:
  - linux
  - server
  - tips
---
warning: Certificate validation failed; consider using the certname configuration option
  
err: Could not retrieve catalog: Certificates were not trusted: certificate verify failed
  
warning: Not using cache on failed catalog

edit
  
/etc/hosts
  
add
  
ip puppet puppet.ur_domain.com 

puppetd &#8211;server puppet.ur_domain.com &#8211;waitforcert 60 &#8211;test