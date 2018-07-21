---
id: 480
title: Nagios Tools for Desktop
date: 2010-01-04T19:08:32+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=480
permalink: /2010-01-nagios-tools-for-desktop/
bttc_cache:
  - 1273324672:0
  - 1273324672:0
categories:
  - linux
tags:
  - monitor
---
If you monitor your system with Nagios, then I&#8217;d like to share a good desktop tool with you.

Nagstamon is a Nagios status monitor which takes place in systray or on desktop (GNOME, KDE, Windows) as floating statusbar to inform you in realtime about the status of your Nagios monitored network. It allows to connect to multiple Nagios servers.

http://sourceforge.net/projects/nagstamon/

Install the necessary tools firstly on Ubuntu 9.10
  
$sudo apt-get install -y python-lxml python-gnome2-extras python-gtkmozembed python-eggtrayicon python-gtkspell python-gksu2 python-gdl python-gda python2.5 libgdl-1-3 libgda-4.0-4 python2.5-minimal libdb4.6 libgdl-1-common libgda-4.0-common
  
$wget http://kent.dl.sourceforge.net/project/nagstamon/nagstamon/nagstamon%200.8.2/nagstamon\_0.8.2\_all.deb
  
$sudo dpkg -i nagstamon\_0.8.2\_all.deb

Enjoy the good tool.