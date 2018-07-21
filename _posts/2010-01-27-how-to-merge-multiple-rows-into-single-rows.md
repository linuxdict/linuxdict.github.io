---
id: 492
title: How to Merge multiple rows into single rows
date: 2010-01-27T20:41:41+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=492
permalink: /2010-01-how-to-merge-multiple-rows-into-single-rows/
bttc_cache:
  - 1273362106:0
  - 1273362106:0
categories:
  - Howto
---
What&#8217;s an easy way to merge multiple rows into single rows? For example, if I have the following:
  
$cat file
      
A
      
B
      
A
      
B
      
A
      
B
  
How can I convert this into:
      
A B
      
A B
      
A B
  
`$awk '{total=total" "$0}NR%2==0{print total; total=""}' file`

I want to be able to merge various numbers of rows into single. In the
  
above example, it&#8217;s 2 rows being merged into 1 but what if I need to
  
merge 3 into 1, such as the following:

A
      
B
      
C
      
A
      
B
      
C

to be converted to the following:
      
A B C
      
A B C
  
`$awk '{total=total" "$0}NR%3==0{print total; total=""}' file`