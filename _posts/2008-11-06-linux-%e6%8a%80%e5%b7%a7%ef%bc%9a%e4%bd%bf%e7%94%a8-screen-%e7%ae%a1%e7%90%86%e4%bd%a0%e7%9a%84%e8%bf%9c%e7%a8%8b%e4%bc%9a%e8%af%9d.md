---
id: 94
title: linux 技巧：使用 screen 管理你的远程会话
date: 2008-11-06T07:00:00+00:00
author: admin
layout: post
guid: http://www.enlamp.cn/?p=71
permalink: '/2008-11-linux-%e6%8a%80%e5%b7%a7%ef%bc%9a%e4%bd%bf%e7%94%a8-screen-%e7%ae%a1%e7%90%86%e4%bd%a0%e7%9a%84%e8%bf%9c%e7%a8%8b%e4%bc%9a%e8%af%9d/'
bttc_cache:
  - 1273300293:0
  - 1273300293:0
categories:
  - 默认
---
http://www.ibm.com/developerworks/cn/linux/l-cn-screen/

screen + 命令

C-a ? 显示所有键绑定信息
  
C-a w 显示所有窗口列表
  
C-a C-a 切换到之前显示的窗口
  
C-a c 创建一个新的运行shell的窗口并切换到该窗口
  
C-a n 切换到下一个窗口
  
C-a p 切换到前一个窗口(与C-a n相对)
  
C-a 0..9 切换到窗口0..9
  
C-a a 发送 C-a到当前窗口
  
C-a d 暂时断开screen会话
  
C-a k 杀掉当前窗口
  
C-a [ 进入拷贝/回滚模式

<span style="font-style: italic;">Lazy Linux: 11 secrets for lazy cluster admins</span>
  
http://www.ibm.com/developerworks/linux/library/l-11sysadtips/index.html

The secrets are

  1. Don&#8217;t reinvent the wheel.
  2. Use open source.
  3. Automate everything.
  4. Design for scale &#8211; plan to be lazy from the start.
  5. Design for hardware manageability.
  6. Use good cluster management software &#8211; don&#8217;t dig wells with teaspoons.
  7. Use open source monitoring solutions.
  8. Control your users with a queuing system.
  9. Verify you get what you pay for &#8211; benchmark it!
 10. Manage cluster communication.
 11. Look for ways to become lazier.