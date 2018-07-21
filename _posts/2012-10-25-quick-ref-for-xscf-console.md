---
id: 764
title: Quick Ref for XSCF console
date: 2012-10-25T18:34:11+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=764
permalink: /2012-10-quick-ref-for-xscf-console/
categories:
  - solaris
tags:
  - solaris
  - tips
---
Final tips: man intro ; then man <command>

List all domain
  
XSCF> showdomainstatus -a

Connect to a domain
  
XSCF> console -d domainhere

Forcely to connect a domain
  
XSCF> console -d domainhere -f

View an connected console
  
XSCF> console -d domainhere -r
  
<!--more-->


  
To displays the domain information specified for a system board.
  
XSCF> showdevices

To displays the temperature, humidity, voltage, and fan rotation speed.
  
XSCF> showenvironment

To lists degraded components.
  
XSCF> showstatus

To displays users who login to the XSCF.
  
XSCF> who

To reset domain there are 3 modes for reset command
  
por: Domain system reset
  
request: Domain panic instruction
  
xir: Domain CPU reset
  
XSCF> reset -d domainhere por

To power on/off all domain or sepcified domain
  
XSCF> poweron
  
XSCF> poweroff

Change the XSCF IP
  
XSCF> setnetwork xscf#0-lan#0 -m netmask your_IP

Remove the Gateway
  
XSCF> setroute -c del -n 0.0.0.0 -g GW xscf#0-lan#0

Add Gateway for XSCF
  
XSCF> setroute -c add -n 0.0.0.0 -g GW xscf#0-lan#0
  
XSCF> applynetwork
  
XSCF> rebootxscf

Display network information
  
XSCF> shownetwork

Display route information
  
XSCF> showroute

To logout of XSCF> type exit
  
To return to XSCF from a domain terminal type #.