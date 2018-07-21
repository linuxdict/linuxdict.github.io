---
id: 872
title: 'How to fix &quot;checkproc: xread error: No such process&quot;'
date: 2009-07-12T21:46:43+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=396
permalink: /2009-07-how-to-fix-checkproc-xread-error-no-such-process-2/
bttc_cache:
  - 1273344710:0
categories:
  - Howto
tags:
  - Howto
  - opensue
  - tips
---
checkproc &#8211; Checks for a process by full path name

this problem is error from crontab, it is also happened on every openSUSE server, if it is installed tripwire
  
the tripwire generate the report. if the server is busy, it will take a long time to finish,
  
but the crontab will run every 15 minutes , if it is done more than 15 mins, maybe it will show the error
  
&#8220;checkproc: checkproc: xread error: No such process&#8221;

-\*/15 \* \* \* * root test -x /usr/lib/cron/run-crons && /usr/lib/cron/run-crons >/dev/null 2>&1
  
/usr/lib/cron/run-crons

line 173:
  
/sbin/checkproc $SCRIPT && continue

btw, it maybe caused by other cron jobs that takes a long time to finish