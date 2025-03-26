---
layout: post
title: '机器人模型URDF'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-25
categories: 传感器
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# <center>雷达部署教程
激光雷达作为机器人重要的传感器，在建图导航等领域具有重要作用
## 1.升级树莓派相关配置

- **更新资源包**
参考学习通--工具资料--2025-3-27-树莓派系统更新.pdf文件，根据教程完成系统更新
## 2.代码验证
- **拷贝雷达驱动**
首先下载雷达驱动，位于学习通--工具资料--雷达ros2驱动包，拷贝到树莓派，解压到工程目录src下（如果你之前创建的工程名称为XXX,则拷贝到XXX/src,和my_base同级目录）
![alt text](/assets/images/lidar-1.png)
- **查看雷达驱动串口号**
```xml
ls /dev/ttyA*
sudo chmod 777 /dev/ttyA*
```
观察雷达驱动使用的串口号，（下一步需要使用）
- **编译**
打开终端，输入以下指令：
```xml
colcon build
```

## 1.创建功能包
