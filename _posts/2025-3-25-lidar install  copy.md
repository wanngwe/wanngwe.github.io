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
- **创建目录**
```xml
cd imu_robot_display
mkdir -p urdf launch rviz
```
- **创建urdf文件**
```xml
touch urdf/imu_robot.urdf
```
编辑文件输入以下内容
```xml
<?xml version="1.0"?>
<robot name="simple_robot">

  <!-- 基础底座 -->
  <link name="base_link">
    <visual>
      <geometry>
        <box size="0.5 0.3 0.1"/>  <!-- 长宽高 -->
      </geometry>
      <material name="red">
        <color rgba="1 0 0 1"/>  <!-- 红色 -->
      </material>
    </visual>
    
    <inertial>
      <mass value="1.0"/>  <!-- 质量1kg -->
      <inertia 
        ixx="0.001" ixy="0.0" ixz="0.0"
        iyy="0.001" iyz="0.0"
        izz="0.001"/>  <!-- 简化惯性矩阵 -->
    </inertial>
  </link>

  <!-- IMU设备 -->
  <link name="imu_link">
    <visual>
      <geometry>
        <box size="0.05 0.05 0.02"/>  <!-- 更小的尺寸 -->
      </geometry>
      <material name="green">
        <color rgba="0 1 0 1"/>  <!-- 绿色 -->
      </material>
    </visual>

    <inertial>
      <mass value="0.1"/>  <!-- 较轻的质量 -->
      <inertia 
        ixx="0.00001" ixy="0.0" ixz="0.0"
        iyy="0.00001" iyz="0.0"
        izz="0.00001"/>
    </inertial>
  </link>

  <!-- 将IMU固定在底座上 -->
  <joint name="imu_joint" type="fixed">
    <parent link="base_link"/>
    <child link="imu_link"/>
    <origin 
      xyz="0.0 0.0 0.06"  
      rpy="0 0 0"/>         <!-- 无旋转 -->
  </joint> 
</robot>
```