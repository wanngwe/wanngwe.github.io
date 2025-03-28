---
layout: post
title: '基于AI设计任务功能包'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-25
categories: 仿真
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# <center>rviz2显示机器人模型教程
AI是一个非常重要的工具，本课程的主要目的在于机器人知识的理解，并不在于编程，故大部分的编程任务我们交给AI完成。以下为三个可以选择的任务，<u>**任选其中一个**</u>:
- **任务1：小车前进1m,后退1m,如此反复**
- **任务2：小车绘制圆形**
- **任务3：设计PID，让小车能准确快速地运行到指定位置处**

基于上述任务，我们生成必要的提示词给AI，比如“我现在有一台全向移动的小车，可以通过订阅/cmd_vel 话题进行控制小车运动，可以通过odom话题观察小车的里程计，请帮我设计一个任务：....,需要python语言，ros2”

机器人软件设计本着一个基本原则：先在仿真系统中运行验证，然后将功能包拷贝到移动机器人平台上验证。
## 1.仿真环境中测试（45分钟）
- **创建空间（已有该空间可以跳过）**
```xml
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```
- **创建包**
```xml
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake my_task \
--dependencies rclcpp robot_state_publisher urdf rviz2
```
- **创建python文件**
```xml
cd src/mytask/mytask
touch mytask.py
```
根据AI生成，编辑文件

- **修改配置文件**
- **修改 package.xml** ，
  ```xml  
  <export>
    <build_type>ament_python</build_type>
  </export> 
  ```
 ament_python后 添加下列依赖项：
```xml
 <exec_depend>rclpy</exec_depend>
 <exec_depend>std_msgs</exec_depend>
```
- **修改setup.py**
打开 setup.py 文件，把 entry_points 字段改为如下内容并保存：
```xml
   entry_points={
        'console_scripts': [
            
           'listener=pynode2.py_sub:main'
        ],
    },
```
- **编译**
进入空间
```xml
cd ~/ros2_ws
colcon build
```
## 2.真实小车上运行
将虚拟机上的功能包拷贝到树莓派相应工程里，假定虚拟机上的功能包为
mytask,树莓派的工程名称为tbot,将mytask文件夹拷贝到tbot/src目录下
编译运行
```xml
colcon build
source install/setup.bash
ros2 run XXX XXX（xxx代表功能包）
```