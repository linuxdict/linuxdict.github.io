---
id: 380
title: Create Ur own Repo for CentOS or RPM base distro
date: 2009-07-03T01:02:10+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=380
permalink: /2009-07-create-ur-own-repo-for-centos-or-rpm-base-distro/
bttc_cache:
  - 1273344710:0
  - 1273344710:0
categories:
  - linux
  - MySQL知识库
tags:
  - linux
  - tips
---
1. create ur own packages, put it into www home directory. let clients can visit from network
  
such as /var/www/html/my_repo
  
http://my\_ip/my\_repo even ftp://my\_ip/my\_repo

2. create u repo files on clients
  
e.g.
  
cat /etc/yum.repos.d/ceph.repo
  
[ceph]
  
name=My Cluster Repo $basearch
  
baseurl=http://my\_ip/my\_repo
  
enabled=1
  
gpgcheck=0 # if u read further, we should change it to &#8220;1&#8221; for security.

3. yum search some_pkgs
  
u should get ur repo now.

<!--more-->


  
advanced for GPG signature.
  
4. #gpg &#8211;gen-key
  
\# if don&#8217;t have gpg , run yum install -y gnupg
  
gpg (GnuPG) 1.4.5; Copyright (C) 2008 Free Software Foundation, Inc.
  
This is free software: you are free to change and redistribute it.
  
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
     
(1) DSA and Elgamal (default)
     
(2) DSA (sign only)
     
(5) RSA (sign only)
  
Your selection? **1**
  
DSA keypair will have 1024 bits.
  
ELG keys may be between 1024 and 4096 bits long.
  
What keysize do you want? (2048) **<return>**
  
Requested keysize is 2048 bits
  
Please specify how long the key should be valid.
           
0 = key does not expire
        
<n> = key expires in n days
        
<n>w = key expires in n weeks
        
<n>m = key expires in n months
        
<n>y = key expires in n years
  
Key is valid for? (0) **<return>**
  
Key does not expire at all
  
Is this correct? (y/N) **y**

You need a user ID to identify your key; the software constructs the user ID
  
from the Real Name, Comment and Email Address in this form:
      
&#8220;Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>&#8221;

Real name: **Edy Liu**
  
Email address: **xfsuper@gmail.com**
  
Comment: Test the GPG sign
  
You selected this USER-ID:
      
&#8220;Edy Liu (Test the GPG sign) <xfsuper@gmail.com>&#8221;

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? **O**
  
You need a Passphrase to protect your secret key.

can&#8217;t connect to \`/root/.gnupg/S.gpg-agent&#8217;: No such file or directory
  
gpg-agent[8794]: You may want to update to a newer pinentry
  
gpg-agent[8794]: You may want to update to a newer pinentry
  
We need to generate a lot of random bytes. It is a good idea to perform
  
some other action (type on the keyboard, move the mouse, utilize the
  
disks) during the prime generation; this gives the random number
  
generator a better chance to gain enough entropy.

**u can type the keyboard &#8230;&#8230;..wait a looooooong time.**

gpg: key E69DC4CC marked as ultimately trusted
  
public and secret key created and signed.
  
gpg: checking the trustdb
  
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
  
gpg: depth: 0 valid: 1 signed: 0 trust: 0-, 0q, 0n, 0m, 0f, 1u
  
pub 1024D/E69DC4CC 2009-07-03
        
Key fingerprint = DB61 772F 74D1 BC7A 2F10 E586 9390 14B2 E69D C4CC
  
uid Edy Liu (Test the GPG sign) <xfsuper@gmail.com>
  
sub 2048g/1CD071D3 2009-07-03

**Now we have our key, that we can use to sign RPM.**
  
\# have a check
  
gpg &#8211;list-keys
  
/root/.gnupg/pubring.gpg
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
  
pub 1024D/E69DC4CC 2009-07-03
  
uid Edy Liu (Test the GPG sign) <xfsuper@gmail.com>
  
sub 2048g/1CD071D3 2009-07-03

edit ~/.rpmmacros

%_signature gpg
  
%\_gpg\_path /root/.gnupg
  
%\_gpg\_name Edy Liu (Test the GPG sign) <xfsuper@gmail.com>
  
%_gpgbin /usr/bin/gpg

cd /var/www/html/my_repo
  
rpm &#8211;addsign *.rpm

5. Make an export of our public key, so users can import it for use with the Repository.
  
gpg &#8211;export -a &#8220;Edy Liu&#8221; > /var/www/html/RPM-GPG-KEY-ENLAMP
  
rpm &#8211;import http://my_ip/RPM-GPG-KEY-ENLAMP
  
****\*\\*\*Very IMPORTANT\*\*\****
  
rm -rf /var/www/html/my_repo/repodata/
  
regenerate the repodata again:
  
createrepo /var/www/html/my_repo**

6. Now yum install -y &#8230;

Maybe some errors:
  
Package does not match intended download
  
yum clean all # on the clients.
  
yum install -y &#8230;