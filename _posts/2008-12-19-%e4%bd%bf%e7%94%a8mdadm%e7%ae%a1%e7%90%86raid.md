---
id: 122
title: 使用mdadm管理Raid
date: 2008-12-19T20:30:58+00:00
author: admin
layout: post
guid: http://blog.enlamp.cn/?p=17
permalink: '/2008-12-%e4%bd%bf%e7%94%a8mdadm%e7%ae%a1%e7%90%86raid/'
bttc_cache:
  - 1273330337:0
  - 1273330337:0
categories:
  - LAMP
---
今天有台数据库服务器不知道怎么出故障了，直接无法进入系统 kernel panic。

是raid5，可是分区有点问题，4块硬盘一块有/boot/  还有raid的一个分区。

也就是 sda2 sdb1 sdc1 sdd1 四部分组成raid5

mdadm 命令解释

mdadm -A /dev/md0

mdadm &#8211;detail /dev/md0

cat /proc/mdstat 检测raid的情况

如果raid里面有资料，不要用 mdadm 创建 raid

mdadm -C /dev/md0 &#8211;level=5 &#8211;raid-devices=4 /dev/sda2 /dev/sdb1 /dev/sdc1 /dev/sdd1

这样的话，内容就挂了

总结：

/boot / 尽量不要放到raid上去。这样恢复比较好一点。