---
id: 774
title: how to fix ldap hange issue on solaris
date: 2012-11-06T21:42:32+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=774
permalink: /2012-11-how-to-fix-ldap-hange-issue-on-solaris/
categories:
  - Howto
  - solaris
---
Issue details:
  
Solaris ldap client doesn&#8217;t work. you can use ldaplist/ldapclient even ps will hang

Solutions:

kill the ldap_cachemgr. 

root # file /var/run/ldap\_cache\_door
  
/var/run/ldap\_cache\_door: door to ldap_cachemgr[1299]

kill 1299

then bounce the ldapclient, more details to trace the issue.
  
<!--more-->

`<br />
root # truss ldaplist<br />
execve("/usr/bin/ldaplist", 0xFFBFFB74, 0xFFBFFB7C)  argc = 1<br />
sysinfo(SI_MACHINE, "sun4v", 257)               = 6<br />
....  = 0<br />
brk(0x0002CC58)                                 = 0<br />
open("/var/run/ldap_cache_door", O_RDONLY)      = 3<br />
fcntl(3, F_SETFD, 0x00000001)                   = 0<br />
door_info(3, 0xFF35A248)                        = 0<br />
door_call(3, 0xFFBFEBB8)        (sleeping...)<br />
^C    Received signal #2, SIGINT, in door_call() [default]</p>
<p>root # file /var/run/ldap_cache_door<br />
/var/run/ldap_cache_door:       door to ldap_cachemgr[1299]</p>
<p>root # ps -ef|grep ldap (hang)<br />
^C<br />
root # ls /proc/1299/<br />
as         ctl        lstatus    object/    psinfo     status<br />
auxv       cwd/       lusage     pagedata   rmap       usage<br />
contracts/ fd/        lwp/       path/      root/      watch<br />
cred       lpsinfo    map        priv       sigact     xmap</p>
<p>root # cat /proc/1299/psinfo<br />
<P¦¦PR¦f<¦" ¦6¦ldap_cachemgr/usr/lib/ldap/ldap_cachemgr¦d¦lUpS(;PR¦[>¦¦TS0¦¦¦¦unwas01c:ConfigureLdap root #</p>
<p>root # svcs |grep ldap<br />
legacy_run     Sep_14   lrc:/etc/rc3_d/S85ldapclient<br />
maintenance     3:54:22 svc:/network/ldap/client:default</p>
<p>root # kill 1299</p>
<p>Nov  7 04:10:43 host01 ls[20489]: libsldap: makeConnection: unable to make LDAP connection, request for a server failed: (Unable to load configuration '/var/ldap/ldap_client_file' ('').)<br />
Nov  7 04:10:43 host01 ls[21109]: libsldap: makeConnection: unable to make LDAP connection, request for a server failed: (Unable to load configuration '/var/ldap/ldap_client_file' ('').)<br />
Nov  7 04:10:43 host01 ls[21323]: libsldap: makeConnection: unable to make LDAP connection, request for a server failed: (Unable to load configuration '/var/ldap/ldap_client_file' ('').)<br />
Nov  7 04:10:43 host01 ls[20911]: libsldap: makeConnection: unable to make LDAP connection, request for a server failed: (Unable to load configuration '/var/ldap/ldap_client_file' ('').)</p>
<p>Total: 2623 processes, 5037 lwps, load averages: 0.22, 0.23, 0.22</p>
<p>root # svcadm clear svc:/network/ldap/client<br />
root # svcs<br />
....<br />
online          4:11:15 svc:/network/ldap/client:default<br />
maintenance    Sep_14   svc:/network/samba:default<br />
maintenance    Sep_14   svc:/network/wins:default</p>
<p>root #<br />
`