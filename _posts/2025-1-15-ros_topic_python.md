---
layout: post
title: 'ROS2话题实验指导书(python)'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-03-16
categories: 实验5---ROS话题实践
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: jekyll 前端开发 设计
author: Dr.wang
---
# 1.创建包

首先进入目录~/ros2_ws/src ，
```xml
cd ~/ros2_ws/src
```
如果没有这个目录，则先创建一个这样的目录，然后进入目录
```xml
mkdir -p ros2_ws/src
cd ~/ros2_ws/src
```
创建一个名为pynode 的包：
```
ros2 pkg create --build-type ament_python pynode
```
# 2.编写发布者节点代码
进入pynode文件夹，新建一个py_pub.py文件
```xml
cd pynode/pynode
touch py_pub.py
```

新建一个py文件，命名为py_pub.py
```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class Talker(Node):
    def __init__(self):
        super().__init__('talker')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        self.timer = self.create_timer(1.0, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = f'Hello, world! {self.i}'
        self.publisher_.publish(msg)
        self.get_logger().info(f'Publishing: "{msg.data}"')
        self.i += 1

def main(args=None):
    rclpy.init(args=args)
    talker = Talker()
    rclpy.spin(talker)
    talker.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
## 2.1代码分析
## 2.2修改package.xml
进入ros2_ws/src/pynode目录并打开package.xml

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

改写完毕后注意记得保存文档!
## 2.3添加入口点
接着打开 setup.py 文件，注意保持如下内容和 package一致
```xml
    maintainer_email='pi@todo.todo',
    description='TODO: Package description',
    license='TODO: License declaration',
```

.把 entry_points 字段改为如下内容并保存，这样程序就知道要运行哪个函数了，即在运行 ros2 run pynode
 talker 命令时，指向 pynode.py_pub:main ：

```xml
 entry_points={
        'console_scripts': [
            'talker=pynode.py_pub:main'
        ],
    },
```
# 3.编写订阅者节点代码
## 3.1新建文件
可以新建一个包pynode2，依照第二部分创建的方法操作（本节内容不进行展示）
```xml
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python pynode2
```
进入pynode2/pynode2创建文件
```
cd ~/ros2_ws/src/pynode2/pynode2
touch py_sub.py
```
并写入以下内容：
```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class Listener(Node):
    def __init__(self):
        super().__init__('listener')
        self.subscription = self.create_subscription(
            String,
            'topic',  # 话题名称
            self.listener_callback,
            10)  # 队列长度
        self.subscription  # 防止未使用变量警告

    def listener_callback(self, msg):
        self.get_logger().info(f'Received: "{msg.data}"')

def main(args=None):
    rclpy.init(args=args)
    listener = Listener()
    rclpy.spin(listener)  # 保持节点运行
    listener.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()

```
## 3.2修改入口点
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
# 4实验观察
## 4.1同时打开两个终端，其中一个终端输入
```
cd ~/ros2_ws
colcon build
source install/setup.bash
ros2 run pynode talker
```
## 4.2 另外一个终端输入
```
cd ~/ros2_ws
colcon build
source install/setup.bash
ros2 run pynode2 listener
```
