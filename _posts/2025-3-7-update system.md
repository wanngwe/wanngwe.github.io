---
layout: post
title: '树莓派---文件传输'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-01
categories: 树莓派
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# <center>树莓派操作----系统更新
烧录的树莓派系统存在部分不足，大家可根据指令进行系统软件更新。
## 1.安装boost库
 ```xml
 sudo apt update
 sudo apt upgrade -y
 sudo apt install libicu-dev=74.2-1ubuntu3 libicu74=74.2-1ubuntu3
 (如果此步失败，请反复尝试)


 ```
## 2.安装 diagnostic-updater

```xml
sudo apt-get install ros-jazzy-diagnostic-updater
```
## 3. 安装 pcap
``` xml
sudo apt install libpcap-dev

```
## 传输机器人模型文件至树莓派
参考文件传输方法（工具资料->树莓派基本操作之传输文件）
将工具资料->移动机器人模型_urdf.rar拷贝到自己工程/src，解压
## 传输 雷达驱动至树莓派
参考文件传输方法（工具资料->树莓派基本操作之传输文件）
将工具资料->雷达ros2驱动包.rar拷贝到自己工程/src，解压
## 编译工程
``` xml
colcon build
```
  
