---
layout: post
title: '机器人模型显示'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-14
categories: 传感器
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# <center>rviz2 显示机器人模型教程
rviz2是一个重要的话题查看工具，可以显示设计的机器人模型，本实验向导阐明具体步骤
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
- **创建启动文件**
```xml
touch launch/display.launch.py
```
打开文件，输入以下内容：
```xml
from launch import LaunchDescription
from launch_ros.actions import Node
from ament_index_python.packages import get_package_share_directory
import os

def generate_launch_description():
    pkg_path = get_package_share_directory('imu_robot_display')
    urdf_file = os.path.join(pkg_path, 'urdf', 'imu_robot.urdf')
    
    return LaunchDescription([
        Node(
            package='robot_state_publisher',
            executable='robot_state_publisher',
            name='robot_state_publisher',
            output='screen',
            arguments=[urdf_file]),
        
        Node(
            package='rviz2',
            executable='rviz2',
            name='rviz2',
            output='screen',
            arguments=['-d', os.path.join(pkg_path, 'rviz', 'config.rviz')])
    ])

```
- **配置空间**
在CMakeLists.txt中添加安装指令：
```xml
install(
  DIRECTORY urdf lanuch
  DESTINATION share/${PROJECT_NAME}
)
```
- **编译**
进入空间
```xml
cd ~/ros2_ws
colcon build
```
## 2.运行
```xml
cd ~/ros2_ws/
source install/setup.bash
ros2 launch imu_robot_display display.launch.py
```
弹出如下界面
![alt text](/assets/images/rvizimage-1.png)
选择 fixed frame ->base_link
选择add->robotmodel ,如图所示
![alt text](/assets/images/rvizimage-2.png)
选择Description topic -->robot description 如图所示
![alt text](/assets/images/rvizimage-3.png)
最终得到如图所示界面
![alt text](/assets/images/rvizimage-5.png)
- **注意**
如果报错未找到robot_state_publisher，请自行安装robot_state_publisher
