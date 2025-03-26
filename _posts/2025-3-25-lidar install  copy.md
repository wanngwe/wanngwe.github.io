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
# <center>rviz2显示机器人模型教程
rviz2是一个重要的话题查看工具，可以显示设计的机器人模型，本实验向导阐明具体步骤
## 1.升级树莓派相关配置

## 1.创建功能包
- **创建空间（已有该空间可以跳过）**
```xml
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```
- **创建包**
```xml
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake imu_robot_display \
--dependencies rclcpp robot_state_publisher urdf rviz2
```