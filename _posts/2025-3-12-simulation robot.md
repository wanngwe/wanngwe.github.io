---
layout: post
title: '机器人虚拟仿真'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-12
categories: ros2
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# <center>全向移动机器人仿真系统
全向移动机器人仿真系统不仅是技术验证的核心工具，更是实现低成本、高效率研发的关键支撑，尤其在动态环境适应性测试具有不可替代性‌。
## 1.配置虚拟机
- **镜像文件位置**
首先确认镜像文件的位置，位于D://robot lecture ros2/ ros2_humble ,在vm虚拟机中打开文件，如图所示
![alt text](/assets/images/无标题.png)
- **修改内存**
为了仿真环境不卡顿，运行流畅，请将虚拟机的内存设置为8GB或者更高，CPU核心设置为16（本次操作只需要执行一次），如图所示
![alt text](/assets/images/无标题1.png)
## 2.运行仿真
- **拷贝仿真工程到虚拟机**
从学习通下载仿真工程文件夹omni_ws.zip，将其传输到虚拟机中，解压（本次操作只需要执行一次）![alt text](/assets/images/16-08-49.png)


- **熟悉仿真工程**
打开omni_ws，我们可以发现其是一个ROS2的功能包，你们有两个脚本文件:clear.sh和rebuild.sh，clear.sh是清除仿真环境脚本，当仿真环境出现异常时运行该脚本，一般不运行。rebuild.sh是编译脚本，一般运行一次即可。如图所示
![alt text](/assets/images/16-10-02.png)
![alt text](/assets/images/16-10-46.png)
- **执行启动**
打开终端，输入以下指令：
```xml
source install/setup.bash
ros2 launch omni_gazebo simulation.py
```
出现如图所示界面
![alt text](/assets/images/16-12-46.png)
## 3.控制
- **控制虚拟机器人运行**
另外打开一个终端，输入
 ```xml
ros2 run teleop_twist_keyboard teleop_twist_keyboard
 ```
 你可以使用这些键来控制机器人的移动和旋转：

箭头键：控制机器人的前后左右移动。
W, A, S, D：分别控制机器人的前进、左转、后退、右转。
I, J, K, L：在全向模式（Holonomic mode）下使用，允许同时控制机器人的前后左右移动。
U, O, J, L：在全向模式下，分别控制机器人的前进、后退、左转、右转。
T, B：分别控制机器人上升和下降。
Q/Z：强制停止机器人。
C：清除到姿势（在某些情况下有用，比如在仿真环境中）。

