---
id: 324
title: I read the following book this weekend
date: 2009-05-17T03:28:30+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=324
permalink: /2009-05-i-read-the-following-book-this-weekend/
bttc_cache:
  - 1273330855:0
  - 1273330855:0
categories:
  - Linux_D
tags:
  - books
  - ruby
---
I read the following book this weekend
  
<Agile Web Development with Rails, 2nd Edition>
  
and do the exam it mentions, but there is a problem.

Q: NoMethodError (undefined method \`scaffold&#8217; for AdminController:Class):
  
A: my rails version is 2.3.2
  
the &#8220;scaffold&#8221; method was removed in Rails 2.0.
  
in order to resolve it , just run the following commands in the app directory
  
script/plugin install scaffolding
  
script/plugin install svn://errtheblog.com/svn/plugins/will_paginate

when u want to practice with the examples, just install the lower version
   
gem install rails &#8211;version 1.2.6 &#8211;include-dependencies