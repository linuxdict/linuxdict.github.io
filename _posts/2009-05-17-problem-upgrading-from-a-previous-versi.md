---
id: 325
title: 'Problem: Upgrading from a previous version'
date: 2009-05-17T03:56:04+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=325
permalink: /2009-05-problem-upgrading-from-a-previous-versi/
bttc_cache:
  - 1273330854:0
  - 1273330854:0
categories:
  - Linux_D
tags:
  - ruby
  - tips
---
Problem:
  
Upgrading from a previous version of Rails to the latest 2.3.2, you get an error:

NameError: uninitialized constant ApplicationController

both in the web browser and in console.

Solution:
  
Since the introduction of Rails 2.3 the application.rb file has been renamed to application_controller.rb.
  
So in order to solve the problem just rename your file application.rb to application_controller.rb.