---
id: 602
title: Top and useful ssh tips
date: 2010-11-26T23:43:37+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=602
permalink: /2010-11-top-and-useful-ssh-tips/
categories:
  - linux
tags:
  - tips
---
1. copy ssh key to remote host
  
`ssh-copy-id user@remote_host`

2 map the tunnel the remote host 80 port to local host port 2001
  
`ssh -N -L2001:localhost:80 remote_host`
  
\# now we can use localhost:2001 to reach remote_host 80

3. compare the local file and remote file
  
`ssh user@host cat /path/to/remotefile | diff /path/to/localfile –`

4. jump point to unreachable_host
  
`ssh -t reachable_host ssh unreachable_host`
  
<!--more-->


  
5. copy file from remote\_host1 to remote\_host2
  
\# please keep in mind, you can reach both remote host
  
`ssh root@remote_host1 "cd /somedir/tocopy/ && tar -cf – ." | ssh root@remote_host2 "cd /samedir/tocopyto/ && tar -xf -"`

6. use screen to keep session alive even disconnected.
  
\# make sure remote_host has screen
  
`ssh -t remote_host screen –r`

7. copy db to new db server with ssh
  
`mysqldump –add-drop-table –extended-insert –force –log-error=error.log -uUSER -pPASS OLD_DB_NAME | ssh -C user@newhost "mysql -uUSER -pPASS NEW_DB_NAME"`

8. remove the &#8220;key change warning&#8221;
  
#actually, this is sed tips 🙂
  
`sed -i 8d ~/.ssh/known_hosts`

9. copy the public key to remote host
  
`cat ~/.ssh/id_rsa.pub | ssh user@remote_host "mkdir ~/.ssh; cat >> ~/.ssh/authorized_keys"`

10. copy huge files to remote host, keep rsync available from both side
  
\# local -> remote
  
`rsync -–partial -avP -–rsh=ssh $file_source $user@$host:$destination_file` 
  
\# remote -> local
  
`rsync –-partial -avP -–rsh=ssh $user@$host:$remote_file $destination_file`