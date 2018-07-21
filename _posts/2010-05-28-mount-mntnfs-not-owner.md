---
id: 567
title: 'mount: /mnt/nfs: Not owner'
date: 2010-05-28T17:34:33+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=567
permalink: /2010-05-mount-mntnfs-not-owner/
categories:
  - solaris
tags:
  - solaris
  - tips
---
nfs mount: mount: /mnt/nfs: Not owner

When you get this error from a Solaris Host, because you are trying to mount an nfsV3 share with an nfsV4 client.

This occurs when you want to share an nfs from a linux host to a solaris host.

Just use the option vers=3 to avoid this problem or configure nfsV4 on the linux host.

mount -o vers=3 linux\_nfs\_01:/htdocs /htdocs