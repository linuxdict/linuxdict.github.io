---
id: 352
title: Rpm error when rpmbuild
date: 2009-07-02T19:29:21+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=352
permalink: /2009-07-rpm-error-when-rpmbuild/
bttc_cache:
  - 1273311935:0
  - 1273311935:0
categories:
  - linux
tags:
  - linux
  - tips
---
I met the problem when i rebuild the ceph

Q: RPM build errors:
      
Installed (but unpackaged) file(s) found:

A: add the files to
  
ur\_package\_name.spec

%file
  
&#8230;..
  
&#8230;..
  
ur files that unpacked