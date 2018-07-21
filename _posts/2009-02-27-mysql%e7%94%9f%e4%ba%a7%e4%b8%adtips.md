---
id: 242
title: MySQL生产中Tips
date: 2009-02-27T23:12:54+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=242
permalink: '/2009-02-mysql%e7%94%9f%e4%ba%a7%e4%b8%adtips/'
bttc_cache:
  - 1273284808:0
  - 1273284808:0
categories:
  - LAMP
---
1、my.cnf的检查工具
      
[mytop](http://jeremy.zawodny.com/mysql/mytop/) [mysqlreport](http://hackmysql.com/mysqlreport)

2、允许mysql query caches

3、Optimize tables 的效果比服务器调整更好一点，如果不能确定优化对象，启动slow query log

4、my.cnf参数调优
  
key_buffer = 20%-50% Physical Ram
  
du -sh \*/\*.MYI 检查index的大小，可以作为决定key_buffer大小的依据

5、调整服务器参数
  
set global key\_buffer\_size=128\*1024\*1024 (即128M)
  
可直接生效
  
修改my.cnf
  
下次启动后生效

5、[更多](http://www.linux-mag.com/id/924)