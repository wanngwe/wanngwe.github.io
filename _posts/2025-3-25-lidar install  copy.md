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

## 3.控制
- **修改端口号**
找到/src/LSLIDAR_X_ROS2-20240228/src/lslidar_driver/params/lidar_uart_ros2/lsn10p.yaml,打开如图所示，修改serial_port_为正确的号
 ```xml
/lslidar_driver_node:
  ros__parameters: 
    frame_id: laser                                       #激光坐标
    group_ip: 224.1.1.2
    add_multicast: false 
    device_ip: 192.168.1.200                   	            #雷达源IP
    device_ip_difop: 192.168.1.102                          #雷达目的ip
    msop_port: 2368                                         #雷达目的端口号
    difop_port: 2369                                        #雷达源端口号
    lidar_name: N10_P                                         #雷达选择:M10 M10_P M10_PLUS M10_GPS N10 L10 N10_P
    angle_disable_min: 120.0                                  #角度裁剪开始值
    angle_disable_max: 230.0                                  #角度裁剪结束值
    min_range: 0.2                                          #雷达接收距离最小值
    max_range: 200.0                                        #雷达接收距离最大值
    use_gps_ts: false                                       #雷达是否使用GPS授时
    scan_topic: /scan                                       #设置激光数据topic名称
    interface_selection: serial                             #接口选择:net 为网口,serial 为串口。
    serial_port_: /dev/ttyACM0                             #串口连接时的串口号
    high_reflection: false                                  #M10_P雷达需填写该值,若不确定，请联系技术支持。
    compensation: false				                              #M10系列是否使用角度补偿功能
    pubScan: true                                           #是否发布scan话题
    pubPointCloud2: false                                    #是否发布pointcloud2话题
    pointcloud_topic: /lslidar_point_cloud 
 ```
- **运行Launch文件**
```xml
colcon build
source install/setup.bash
ros2 launch lslidar_driver lsn10p_launch.py
```
另开开一个终端，查看scan话题
```xml
ros2 topic echo /scan
```
![alt text](/assets/images/lidar-2.png)
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


