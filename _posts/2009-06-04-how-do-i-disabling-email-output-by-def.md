---
id: 339
title: How do I disabling Email output?
date: 2009-06-04T18:32:55+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=339
permalink: /2009-06-how-do-i-disabling-email-output-by-def/
bttc_cache:
  - 1273340062:0
  - 1273340062:0
categories:
  - linux
tags:
  - linux
  - server
  - tips
---
How do I disabling Email output?

By default the output of a command or a script (if any produced),
  
will be email to your local email account.
  
To stop receiving email output from crontab you need to append >/dev/null 2>&1.
  
For example:0 3 \* \* * /root/backup.sh >/dev/null 2>&

To mail output to particluer email account let us say vivek@nixcraft.in
  
you need to define MAILTO variable to your cron job:
  
MAILTO=&#8221;vivek@nixcraft.in&#8221;
  
0 3 \* \* * /root/backup.sh >/dev/null 2>&1

More details:
  
http://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/