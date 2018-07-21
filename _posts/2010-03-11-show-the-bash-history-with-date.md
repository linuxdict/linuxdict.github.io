---
id: 504
title: Show the Bash History with date
date: 2010-03-11T18:14:39+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/2010-03-show-the-bash-history-with-date/
permalink: /2010-03-show-the-bash-history-with-date/
bttc_cache:
  - 1273362105:0
  - 1273362105:0
categories:
  - Linux_D
---
`echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile`

Finished 🙂
  
run history command, the output should looks like the following.
  
1014 12/03/10 01:13:44 who -r
  
1015 12/03/10 01:13:45 history