---
id: 684
title: Important Server Maintenance/Update Notes from RH
date: 2011-08-02T18:14:24+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=684
permalink: /2011-08-important-server-maintenanceupdate-notes-from-rh/
categories:
  - linux
---
First, the most important thing is to perform system update in a maintenance window, because if you have any critical service, the service must be stopped before the upgrade begins.

The maintenance window is also necessary because the server needs a reboot to the new kernel goes into production.

If the server has some third-party module into the kernel, the inclusion of these modules should also be made for the new kernel, otherwise the new kernel will not contain all the modules required and this can cause problems at boot process and devices&#8217; recognition, such as storage, drive controllers, and others&#8230;
  
<!--more-->


  
If the server faces any problems with the new kernel after rebooting, it is possible reboot the server using the old kernel as a workaround.

It is highly recommended perform a backup of the configuration files of the most critical services, because if a problem occurs with the updated version of the packages, you can a package downgrade using the command &#8220;yum downgrade <packagename>&#8221; and restore the saved configurations.

If your server has any third-party applications installed, such as Oracle, will be necessary check with software vendor if application is certified for the version that system will assumes after updated.

It is recommended that you apply all changes and updates in a test environment first for approval before perform the upgrade in production servers, so you can avoid future problems.