---
id: 630
title: Changing password inside a script
date: 2011-06-08T21:43:53+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=630
permalink: /2011-06-changing-password-inside-a-script/
categories:
  - Howto
tags:
  - tips
---
In an ideal world you&#8217;d never need to change the password associated with a user account without using passwd, but there are times when it is helpful to script such things.

The naive attempts to automate the use of passwd will fail, so the standard advice has always been to use a tool like expect to interactively call the passwd binary.

But there is an alternative approach which is more sensible which is to use the usermod command to change a password.

Assume you have a user account called guest upon your system and you wish to set the user&#8217;s password to openaccess you can do this by running:

\# hash=$(echo openaccess | openssl passwd -1 -stdin)
  
\# usermod &#8211;pass=&#8221;$hash&#8221; guest

If you wish you could combine that into a single line:

\# usermod -p $(echo openaccess | openssl passwd -1 -stdin) guest

If a local user can see the commands you&#8217;re running in the output of &#8220;ps&#8221;, &#8220;top&#8221;, or similar then this is insecure &#8211; but if you generate the hash remotely you should probably be safe enough.