---
layout: post
title: '树莓派系统制作'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-01-01
categories: 实验5---ROS话题实践
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---

准备一张空白SD卡，格式化SD卡，
将SD卡插入到树莓派上
使用umount 挂载
使用命令  dd bs=4M if=/dev/mmcblk0 of=/dev/sda 将树莓派系统内容全部拷贝到SD卡上，
其中mmcblk0是树莓派上系统卡，sda是插入的SD卡，使用lsblk查看，等待完成后既可以将SD卡插入到树莓派上。