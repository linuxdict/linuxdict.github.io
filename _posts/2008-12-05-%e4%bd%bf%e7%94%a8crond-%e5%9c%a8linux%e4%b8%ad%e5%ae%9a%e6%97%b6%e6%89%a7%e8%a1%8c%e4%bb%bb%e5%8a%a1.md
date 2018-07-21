---
id: 23
title: 使用crond 在linux中定时执行任务
date: 2008-12-05T09:33:28+00:00
author: lele
excerpt: 使用crond 在linux中定时执行任务
layout: post
guid: http://xfsuper.gicp.net/blog/?p=23
permalink: '/2008-12-%e4%bd%bf%e7%94%a8crond-%e5%9c%a8linux%e4%b8%ad%e5%ae%9a%e6%97%b6%e6%89%a7%e8%a1%8c%e4%bb%bb%e5%8a%a1/'
bttc_cache:
  - 1273294871:0
  - 1273294871:0
categories:
  - linux
---
定期运行程序或者脚本是管理员要面临一个很普遍的问题
  
一、 使用crond监控程序运行程序
  
1. 使用cron来定期执行任务
  
使用crond (cron监控程序)来定期运行一些任务，比如备份日志、数据库、把日志发送到自己邮箱等等操作都可以又定期运行程序来完成。<!--more-->


  
crond是个脚本，每次Linux启动的时候都自动起到该脚本，该脚本是 /etc/rc.d/init.d 下面的，每次系统启动的时候就自动会启动该目录下的脚本。
  
cron有两个配置文件，一个/etc/crontab，是一个全局配置文件，一组是crontab命令生成生成的配置文件，是属于用户级的。
  
一般对管理员来说，只要使用全局配置的/etc/crontab就配置文件就可以了，我们去打开配置文件看看：
  
SHELL=/bin/bash
  
PATH=/sbin:/bin:/usr/sbin:/usr/bin
  
MAILTO=root
  
HOME=/
  
\# run-parts
  
01 \* \* \* \* root run-parts /etc/cron.hourly
  
02 4 \* \* * root run-parts /etc/cron.daily
  
22 4 \* \* 0 root run-parts /etc/cron.weekly
  
42 4 1 \* \* root run-parts /etc/cron.monthly
  
我们稍微来分析一下这个文件：
  
/\* 设置基于什么shell来运行，我们这里是基于bash shell \*/
  
SHELL=/bin/bash
  
/\* 指定目录中有次文件的命令时，不需要完整目录路经 \*/
  
PATH=/sbin:/bin:/usr/sbin:/usr/bin
  
/\* 使用cron实际工作时，见通过邮件来同志root用户 \*/
  
MAILTO=root
  
/\* 与/etc/crontab配置文件相关的主目录为根目录 \*/
  
HOME=/
  
/\* 好了，这里是关键是，下面的是要指定什么时间运行什么目录下的任务，run-parts命令是运行指定目录下的每个脚本 \*/
  
\# run-parts
  
/\* 这一句是在每天每小时过后一分钟运行/etc/cron.hourly目录中的每个脚本文件 \*/
  
01 \* \* \* \* root run-parts /etc/cron.hourly
  
/\* 在每天凌晨4点2分运行/etc/cron.daily目录中的每个脚本文件 \*/
  
02 4 \* \* * root run-parts /etc/cron.daily
  
/\* 在每个星期天凌晨4点22分运行/etc/cron.weekly目录中的每个脚本文件 \*/
  
22 4 \* \* 0 root run-parts /etc/cron.weekly
  
/\* 在每个月的第一天凌晨4点42分运行/etc/cron.monthly目录中的每个脚本文件 \*/
  
42 4 1 \* \* root run-parts /etc/cron.monthly
  
大家看到里面的&#8221;*&#8221;一定觉得很奇怪，下面我们句稍微来了解一下cron的语法：
  
上面脚本中的时间是从左到右的，分别列出了五个字段，我们看下面的表：
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
  
字段 取值范围
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
  
Minute 0 ~ 59
  
Hour 0 ~ 23，其中0是午夜，20是晚上8点
  
Day 1 ~ 31
  
Month 1 ~ 12
  
Day of week 0 ~ 7，其中0和7是表示星期天
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
  
任何字段中的星号是通配符，例如，如果第一个字段包括星号，则特定若无其事在可能的每一分钟运行。如果要指定时间范围，比如上午8点到
  
下午4点，则可以见第二个字段设置为8~16。如果要隔一天运行任务，则可以将第三个字段设置为*/2。可以看出，如果五个字段(minute、hour
  
、day、month、day of week) 之后，cron中的每个字段就没什么神秘之处了。

2. 用户自己的cron
  
用户也可以计划用户自己的cron任务，比如他想要在半夜整理他的文件，然后发送邮件给自己，只要这个用户他没有在/etc/cron.deny表中，
  
就可以使用crontab -e命令来启动自己的cron文件。
  
3. 对cron的访问控制
  
默认情况下，所有用户都能访问cron工具，要对cron进行访问控制，则可以生成/etc/cron.allow与/etc/cron.deny文件。
  
(1)这两个文件都不存在时，每个用户都可以访问cron工具]
  
(2)存在/etc/cron.allow文件时，则只有cron.allow文件中允许的用户才能访问cron工具，如果也有/etc/cron.deny文件，则忽略cron.deny文
  
件

二、 使用at命令定期运行程序
  
1. 使用cron运行任务
  
cron任务的缺点是计划要经常运行，假如我们只是想要让特定任务运行一次呢？那么，这时候就要用到at监控程序了。
  
设置at命令很简单，指示定运行的时间，那么就会在哪个时候运行。at类似打印进程，会把任务放到/var/spool/at目录中，到指定时间运行它
  
。at命令相当于另一个shell，运行at time命令时，它发送一个个命令，可以输入任意命令或者程序。at now + time命令可以在指示任务。
  
假设处理一个大型数据库，要在别人不用系统时去处理数据，比如凌晨2点5分。那么我们就应该先建立/home/mj/airplane脚本管理数据库，计
  
划处理/home/mj/air-safe文件中的结果。正常方式是这样启动下列命令:
  
\# at 2:05 tomorrow
  
at> /home/mj/airplane > /home/mj/air-safe
  
at> Ctrl+D
  
AT Time中的时间表示方法
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;
  
时间 例子 说明
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;
  
Minute at now + 5 minutes 任务在5分钟后运行
  
Hour at now + 1 hour 任务在1小时后运行
  
Days at now + 3 days 任务在3天后运行
  
Weeks at now + 2 weeks 任务在两周后运行
  
Fixed at midnight 任务在午夜运行
  
Fixed at 10:30pm 任务在晚上10点3