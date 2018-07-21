---
id: 740
title: Auto-deploy Hadoop cluster with HDP
date: 2012-06-22T20:16:47+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=740
permalink: /2012-06-auto-deploy-hadoop-cluster-with-hdp/
categories:
  - Howto
tags:
  - hadoop
---
With the heat of Hadoop, the deployment and monitor becoming our system engineers&#8217; focus.
  
More solution coming out now. such as Serengeti, but it aims for the Vsphere.
  
Bigtop, is a project under Apache. not bad, will give it a try.
  
HDP, Hortonworks Data Platform has been release recently. 

Will try mention as much details doing the installation as I can.
  
<!--more-->


  
Preparation:
  
1. OS, Although HDP offically support CentOS 5.x/ RHEL 5.x. we still found some issue when doing the installation.
  
such as missing nodes when doing the deployment(can be fixed by update php5.1 to php5.3 but will bring more issue).
  
so we skip CentOS 5.x and use CentOS 6.x. it&#8217;s cool and have less issue ;), recommend install the OS with minimal packages.
  
\# tips, please update the release file.
  
sed -i.bak &#8216;s/6.2/5.8/g&#8217; /etc/redhat-release

2. Disable Selinux and Iptables.
  
/etc/sysconfig/selinux SELINUX=disabled
  
chkconfig iptables off
  
reboot

3. password less auth
  
ssh-keygen
  
ssh-copy-id target_host (don&#8217;t forget the deployment host itself.)

4. DNS, add the new nodes to DNS with PTR record. or you can add them to /etc/hosts. 

Start Installation:

1. Enable Repo
  
\# ruby repo
  
rpm -Uvh http://passenger.stealthymonkeys.com/rhel/6/passenger-release.noarch.rpm
  
\# HDP
  
rpm -Uvh http://public-repo-1.hortonworks.com/HDP-1.0.0.12/repos/centos5/hdp-release-1.0.0.12-1.el5.noarch.rpm
  
\# EPEL
  
rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-7.noarch.rpm

2. Install HMC (HDP core package)
  
Note: when you start the HMC. it ask you download JDK. recommend download by yourself from Oracle site.

[root@hmhdp01 ~]# yum install -y hmc php-process
  
[root@hmhdp01 ~]# service hmc start
  
Do you agree to Oracle&#8217;s Java License at
  
/usr/share/hmc/licenses/ORACLE\_JDK\_LICENSE.txt?(y/n)y
  
Would you like us to download the JDK binaries for you?(y/n)n
  
Please download jdk-6u31-linux-x64.bin and jdk-6u31-linux-i586.bin from Oracle to /var/run/hmc/downloads/
  
Starting HMC Installer [ OK ]
  
Starting httpd:
  
Starting HMC
  
3. Deploy HDP.
  
3.1
  
\# update puppet for the nagios. remove php-pecl-json. because php5.3 already include it by default.
  
line 11+ /etc/puppet/master/modules/hdp-nagios/manifests/server/packages.pp
  
3.2
  
open http://your\_deploy\_host/hmc/html/

Then next follow the guide. Good luck.

Snapshots:
  
[<img class="alignnone size-full wp-image-117" title="Hortonworks Management Center-142939" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-142939.png" alt="" width="600" height="450" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-142939.png)

[<img class="alignnone size-full wp-image-114" title="Hortonworks Management Center-182821" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-182821.png" alt="" width="600" height="470" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-182821.png)

[<img class="alignnone size-full wp-image-118" title="Hortonworks Management Center-211324" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-211324.png" alt="" width="600" height="520" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-211324.png)

[<img class="alignnone size-full wp-image-121" title="Hortonworks Management Center-201936" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-201936.png" alt="" width="600" height="500" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-201936.png)

[<img class="alignnone size-full wp-image-122" title="Hortonworks Management Center-201952" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-201952.png" alt="" width="600" height="520" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-201952.png)

[<img class="alignnone size-full wp-image-123" title="Hortonworks Management Center-202007" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-202007.png" alt="" width="600" height="480" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-202007.png)

[<img class="alignnone size-full wp-image-124" title="Hortonworks Management Center-202008" src="http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-202008.png" alt="" width="600" height="330" />](http://www.cnlinuxgeek.com/wp-content/uploads/2012/06/Hortonworks-Management-Center-202008.png)