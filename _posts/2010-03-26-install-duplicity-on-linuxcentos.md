---
id: 512
title: Install Duplicity on Linux(CentOS)
date: 2010-03-26T02:06:22+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=512
permalink: /2010-03-install-duplicity-on-linuxcentos/
bttc_cache:
  - 1273362104:0
  - 1273362104:0
categories:
  - Howto
  - Linux_D
---
Duplicity backs directories by producing encrypted tar-format volumes
  
and uploading them to a remote or local file server.

Firstly, enable two important repo

<blockquote class="wp-embedded-content" data-secret="PvE9TnagXg">
  <p>
    <a href="http://192.168.1.77:8880/2009-06-enable-two-important-repo-for-centos-5/">Enable two important repo for CentOS 5</a>
  </p>
</blockquote>



Secondly, install Duplicity
  
$sudo yum install -y duplicity

Finally, Use it.
  
$duplicity &#8211;help 

Following is a short tutorial
  
<!--more-->


  
e.g.
  
#I already put the keys in master.linuxdict.com, so I don&#8217;t need a password here.
  
$duplicity test/ scp://root@master.linuxdict.com/tmp
  
GnuPG passphrase:
  
Local and Remote metadata are synchronized, no sync needed.
  
Last full backup date: none
  
No signatures found, switching to full backup.
  
&#8212;&#8212;&#8212;&#8212;&#8211;[ Backup Statistics ]&#8212;&#8212;&#8212;&#8212;&#8211;
  
StartTime 1269593213.36 (Fri Mar 26 02:46:53 2010)
  
EndTime 1269593213.67 (Fri Mar 26 02:46:53 2010)
  
ElapsedTime 0.31 (0.31 seconds)
  
SourceFiles 3
  
SourceFileSize 3060258 (2.92 MB)
  
NewFiles 3
  
NewFileSize 3060258 (2.92 MB)
  
DeletedFiles 0
  
ChangedFiles 0
  
ChangedFileSize 0 (0 bytes)
  
ChangedDeltaSize 0 (0 bytes)
  
DeltaEntries 3
  
RawDeltaSize 3056162 (2.91 MB)
  
TotalDestinationSizeChange 3067132 (2.93 MB)
  
Errors 0
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

\# On master.linuxdict.com
  
$ls ~/tmp/
  
duplicity-full.20100326T084637Z.manifest.gpg
  
duplicity-full.20100326T084637Z.vol1.difftar.gpg
  
duplicity-full-signatures.20100326T084637Z.sigtar.gpg
  
&#8230;
  
$file tmp/duplicity-full.20100326T084637Z.vol1.difftar.gpg
  
tmp/duplicity-full.20100326T084637Z.vol1.difftar.gpg: DOS executable (COM)
  
\# so others can&#8217;t easily copy it. 🙂
  
&#8212;
  
\# Other useful command
  
\# backup incrementally
  
$duplicity incr test/ scp://root@master.linuxdict.com/tmp
  
\# check the files that has been backuped.
  
$duplicity list-current-files scp://root@master.linuxdict.com/tmp
  
\# Restore all the backup
  
$duplicity restore scp://root@master.linuxdict.com/tmp
  
\# Restore only the file we need
  
$duplicity restore &#8211;file-to-restore wiki\_import-1.1.tgz scp://root@master.linuxdict.com/tmp /root/wiki\_import-1.1.tgz

More details:
  
RTFM 🙂 and http://www.nongnu.org/duplicity/ (offical site)