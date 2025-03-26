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
编辑文件
[查看完整URDF文件](/assets/file/robot.urdf)

- **创建启动文件**
```xml
touch launch/display.launch.py
```
打开文件，输入以下内容：

```
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
