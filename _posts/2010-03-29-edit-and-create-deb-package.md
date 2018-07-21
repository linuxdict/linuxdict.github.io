---
id: 521
title: Edit and create deb package
date: 2010-03-29T01:09:54+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=521
permalink: /2010-03-edit-and-create-deb-package/
bttc_cache:
  - 1273363924:0
  - 1273363924:0
categories:
  - Howto
  - linux
---
1. Unpack the Deb with the following line
  
mkdir temp; dpkg-deb &#8211;extract mypack.deb temp

What is being done to the left of the, is to create a directory
  
where temporary unpacking the deb. On the right, is specified
  
that unpacking the deb in the directory you created earlier.

2. Now extracting control package temporary / DEBIAN with the following line:
  
dpkg-deb &#8211;control mypack.deb temp/DEBIAN

3. Now edit the temporary file / DEBIAN / control changes fights that we want.

4. The repackaging. Deb with the following line:
  
dpkg &#8211;build temp; get your new pack.deb

5. Now we can install our new package with the command
   
sudo dpkg -i mypack.deb