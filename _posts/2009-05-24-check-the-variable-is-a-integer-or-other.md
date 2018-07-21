---
id: 329
title: Check the variable an integer
date: 2009-05-24T21:48:39+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=329
permalink: /2009-05-check-the-variable-is-a-integer-or-other/
bttc_cache:
  - 1273350184:0
  - 1273350184:0
categories:
  - linux
tags:
  - Shell
  - tips
---
Check the variable is a integer or others.

#!/bin/bash

read Nau
  
if [ &#8220;${Nau//[^0-9]/}&#8221; == &#8220;$Nau&#8221; ]; then
	  
echo &#8220;$Nau Is a number&#8221;;
  
else
	  
echo &#8220;$Nau is not a number&#8221;
  
fi