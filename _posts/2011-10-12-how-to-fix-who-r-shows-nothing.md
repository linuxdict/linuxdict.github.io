---
id: 695
title: 'how to fix &#8216;who -r&#8217; shows nothing'
date: 2011-10-12T19:05:53+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=695
permalink: /2011-10-how-to-fix-who-r-shows-nothing/
categories:
  - solaris
tags:
  - solaris
  - tips
---
OS: Solaris 9.
  
Issue: who -r won&#8217;t give you the running level. so the pkgadd won&#8217;t work.
  
myhost1:~ root # who -r # shows no output

Solution:
  
check the /var/adm/utmpx, maybe the file has been corrupted
  
myhost1:~ root # cd /var/adm
  
myhost1:adm root # vi u1.log
  
\# paste the following content.
                                        
system boot 0 2 0000 0000 1315335814 0 0 0 Tue Sep 6 20:03:34 2011
                                        
run-level 3 0 1 0063 0123 1315335839 0 0 0 Tue Sep 6 20:03:59 2011
  
rc2 s2 1262 8 0000 0000 1315335885 0 0 0 Tue Sep 6 20:04:45 2011
  
rc3 s3 3938 8 0000 0000 1315335915 0 0 0 Tue Sep 6 20:05:15 2011
  
<!--more-->


  
myhost1:adm root # cat u1.log
                                        
system boot 0 2 0000 0000 1315335814 0 0 0 Tue Sep 6 20:03:34 2011
                                        
run-level 3 0 1 0063 0123 1315335839 0 0 0 Tue Sep 6 20:03:59 2011
  
rc2 s2 1262 8 0000 0000 1315335885 0 0 0 Tue Sep 6 20:04:45 2011
  
rc3 s3 3938 8 0000 0000 1315335915 0 0 0 Tue Sep 6 20:05:15 2011
  
myhost1:adm root # /usr/lib/acct/fwtmp -ic < u1.log > /var/adm/utmpx
  
myhost1:adm root # who -r
     
. run-level 3 Sep 6 20:03 3 0 S

If paste to the u1.log won&#8217;t work properly. you can find another normal server. run
  
/usr/sbin/acct/fwtmp < /var/adm/utmpx > u1.log
  
and scp to the broken host.

Details on wtmpx.
  
fwtmp manipulates connect-time accounting records by reading binary records in wtmp format from standard input, converting them to formatted ASCII records. The ASCII version is useful when it is necessary to edit bad records.

\# fwtmp [-ic]

where :

-ic : denotes that input is in ASCII form, and output is to be written in binary form.

Example to convert a binary record in wtmp format to an ASCII record called dummy.file, enter:

#fwtmp < /var/adm/wtmp > dummy.file

Example to convert an ASCII dummy.file to a binary file in wtmp format called /var/adm/wtmp, enter the fwtmp command with the -ic switch:

#fwtmp -ic < ascii.file > /var/adm/wtmp

Note: Depending on your flavour of Unix, the file may be called wtmpx or wtmp.

fwtmp also can be used to modify utmpx or utmp.