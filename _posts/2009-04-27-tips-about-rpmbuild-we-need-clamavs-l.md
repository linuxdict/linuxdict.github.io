---
id: 298
title: tips about rpmbuild
date: 2009-04-27T01:16:18+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=298
permalink: /2009-04-tips-about-rpmbuild-we-need-clamavs-l/
bttc_cache:
  - 1273290411:0
  - 1273290411:0
categories:
  - Linux_D
tags:
  - tips
---
tips about rpmbuild

we need clamav&#8217;s libraries for havp-0.90-1.x86_64.rpm
  
the library file is libclamav.so.6
  
and don&#8217;t want the update make havp crash ( havp is rpmbuild rebuilt from source)
  
so when I rebuild the rpm i use the following options(edit havp.spec):

Requires: clamav
  
Provides: libclamav.so.6

firstly meet the clamav then match libclamav.so.6;
  
so we won&#8217;t care the clamav version, just if it provides the libclamavi.so.6. we can use it.

more details on rpmbuild
  
http://www.rpm.org