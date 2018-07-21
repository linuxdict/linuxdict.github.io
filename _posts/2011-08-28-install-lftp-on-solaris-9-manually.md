---
id: 692
title: Install Lftp on Solaris 9 manually
date: 2011-08-28T23:41:37+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=692
permalink: /2011-08-install-lftp-on-solaris-9-manually/
categories:
  - solaris
---
Yeah, there is pkg-get way.
  
If you don&#8217;t have pkg-get, you can follow the steps.

wget ftp://ftp.sunfreeware.com/pub/freeware/sparc/9/lftp-4.0.10-sol9-sparc-local.gz
  
wget ftp://ftp.sunfreeware.com/pub/freeware/sparc/9/readline-5.2-sol9-sparc-local.gz
  
wget ftp://ftp.sunfreeware.com/pub/freeware/sparc/9/libgcrypt-1.4.6-sol9-sparc-local.gz
  
<!--more-->


  
wget ftp://ftp.sunfreeware.com/pub/freeware/sparc/9/libgpgerror-1.10-sol9-sparc-local.gz
  
wget http://sourceforge.net/apps/trac/gar/export/13001/csw/mgar/pkg/gnutls/branches/libgnutls13/files/gnutls-2.0.4-2009.01.22-sparc-libgnutls.so.13.9.1
  
cp gnutls-2.0.4-2009.01.22-sparc-libgnutls.so.13.9.1 /usr/local/lib/
  
ln -s gnutls-2.0.4-2009.01.22-sparc-libgnutls.so.13.9.1 libgnutls.so.13
  
pkgadd -d ./libgpgerror-1.10-sol9-sparc-local
  
pkgadd -d ./libgcrypt-1.4.6-sol9-sparc-local
  
pkgadd -d ./readline-5.2-sol9-sparc-local
  
pkgadd -d ./lftp-4.0.10-sol9-sparc-local

ldd /usr/local/bin/lftp
          
libexpat.so.1 => /usr/local/lib/libexpat.so.1
          
libgnutls.so.13 => /usr/local/lib/libgnutls.so.13