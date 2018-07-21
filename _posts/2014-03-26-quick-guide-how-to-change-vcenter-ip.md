---
id: 833
title: 'Quick guide: How to change Vcenter IP'
date: 2014-03-26T18:55:12+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=833
permalink: /2014-03-quick-guide-how-to-change-vcenter-ip/
categories:
  - Linux_D
tags:
  - vmware
---
Simple way, update before you move it away.
  
Admininstrate -> vCenter Server setting -> Advanced Settings.

I installed Vcenter on a VM. so I did clone. but the IP need to be updated. 

because the SSO still try to find the old IP. updated many configuration files, still stucks.
  
<!--more-->

014-03-27T17:37:45.350+08:00 \[05060 error &#8216;HttpConnectionPool-000001&#8217;\] \[ConnectComplete\] Connect failed to <cs p:0000000009637d70, TCP:10.60.254.248:7444>; cnx: (null), error: class Vmacore::Ssl::SSLVerifyException(SSL Exception: Verification parameters:
  
&#8211;> PeerThumbprint: 4B:2A:96:C3:45:C8:A9:30:AD:2B:46:AD:50:60:29:40:F3:B6:77:94
  
&#8211;> ExpectedThumbprint:
  
&#8211;> ExpectedPeerName: 10.x.x.x
  
&#8211;> The remote host certificate has these problems:
  
&#8211;>
  
&#8211;> * A certificate in the host&#8217;s chain is based on an untrusted root.
  
&#8211;>
  
&#8211;> * Host name does not match the subject name(s) in certificate.)
  
2014-03-27T17:37:45.351+08:00 \[02320 error &#8216;[SSO\]\[SsoFactory_CreateFacade\]&#8217;] Unable to create SSO facade: SSL Exception: Verification parameters:
  
&#8211;> PeerThumbprint: 4B:2A:96:C3:45:C8:A9:30:AD:2B:46:AD:50:60:29:40:F3:B6:77:94
  
&#8211;> ExpectedThumbprint:
  
&#8211;> ExpectedPeerName: 10.x.x.x
  
&#8211;> The remote host certificate has these problems:
  
&#8211;>
  
&#8211;> * A certificate in the host&#8217;s chain is based on an untrusted root.
  
&#8211;>
  
&#8211;> * Host name does not match the subject name(s) in certificate..
  
2014-03-27T17:37:45.352+08:00 \[02320 error &#8216;vpxdvpxdMain&#8217;\] \[Vpxd::ServerApp::Init\] Init failed: Vpx::Common::Sso::SsoFactory_CreateFacade(sslContext, ssoFacadeConstPtr)
  
&#8211;> Backtrace:

Ref: http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2058080

I followed guide from VM site. still can&#8217;t fixed my problem. so I created an dummy network interface, and with old IP. then all looks fine. you can go vcenter to change IP now.

Files related with IP:
  
C:\Program Files\VMware\Infrastructure\VirtualCenter Server\ssoregtool\vcsso.properties
  
C:\Program Files\VMware\Infrastructure\VirtualCenter Server\endpoints\qs-endpoint.xml
  
C:\Program Files\VMware\Infrastructure\Orchestrator\vco.properties
  
C:\ProgramData\VMware\VMware VirtualCenter\vpxd.cfg

Useful logs:
  
C:\ProgramData\VMware\VMware VirtualCenter\Logs