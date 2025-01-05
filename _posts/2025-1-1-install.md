---
layout: post
title: '机器人装配指导书'
subtitle: '或许是最漂亮的Jekyll主题'
date: 2025-01-04
项目: 实验1---机器人装配
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
#tags: 组装 调试
---
# 三轮小车的组装过程

![总装效果](/assets/images/总装效果.jpg)

------

[TOC]

------

## 三轮小车全部物料准备:

**大部件物料：**

| 部件                                            | 数量（个） |
| :---------------------------------------------- | ---------- |
| 亚克力车身：底板、中板、顶板                    | 各1个      |
| 2D雷达：N10P                                    | 1          |
| 上位机：树莓派4B或5                             | 1          |
| 下位机：轮趣的C30D（ROS主控）板子               | 1          |
| 轮趣MG513P30电机（GMR编码器 or 霍尔编码器电机） | 3          |
| 全向轮：轮趣的omni b60 ，安装孔径选择6mm        | 3          |
| 12V电池                                         | 1          |
| 3D打印OLED支架                                  | 1          |
| 3D打印雷达支架                                  | 1          |
| 3D打印电池仓                                    | 1          |
| 3D打印电机支架                                  | 3          |

**小部件物料：**

| 部件                                                         | 数量（个） |
| ------------------------------------------------------------ | ---------- |
| DC供电线                                                     | 1          |
| OLED的延长线：**杜邦线2.54  21cm**                           | 6          |
| 双通道铜柱M3 * 40mm（底板与中板支撑）                        | 4          |
| 双通道铜柱（中板与顶板支撑）：M3*70mm                        | 4          |
| 双通道铜柱（雷达支撑）：M3 *30mm                             | 4          |
| 双通道铜柱（固定C30D、树莓派、OLED支架固定）：M3*10mm        | 10         |
| 双通道铜柱（固定雷达串口转接板）：M2 * 10mm                  | 8          |
| [转接铜柱（单通道）（树莓派）：M3*4+3(内螺纹2.5)](https://item.taobao.com/item.htm?_u=1209sl7oamb1f6&id=676872916227&spm=a1z09.2.0.0.44482e8dZVD6Cx&skuId=5038903783857) | 4          |
| 螺丝(固定电池仓)：M3 * 16mm                                  | 4          |
| 螺丝（固定电机和电机支架）：M3 *10mm（十字槽沉头）           | 约21       |
| 螺丝（连接铜柱）：M3 * 6mm                                   | 约40       |
| 螺丝（固定树莓派转接铜柱）：M2.5 *5mm（十字槽沉头）          | 4          |
| 螺丝（固定雷达串口转接板铜柱）：M2*5mm（十字槽沉头）         | 8          |
| 螺丝（OLED连接支架）：M2*6mm                                 | 6          |
| [内六角螺丝（雷达固定，螺丝头部直径3.8mm左右）：M2*16mm](https://detail.tmall.com/item.htm?abbucket=20&id=635755541429&ns=1&pisk=fKWSKQ0Tw405FUPz1DE2lWSCQRvCRwwZPDtdjMHrvLpJJssGRUr3ZL5XRZQXyYruZBLCrLdhae8yRpsh5ozaQRSlqpA87PyatnbUdd0-2Y3EHIK6ZrrquRSlqpmSJl5YQ2ZcJwDK9eQpHIKBjpKJ2bLYcHt6JpLJ9qhvXEppJwLpkEKev3KppQEjMHKsybKJ2npvjHoJppQdDvFrfHNWrgZVLePLcRV5fEMKCcx9w7jSTvDhN3d5Qi8X0nWXVQT6gJ9OZTQVvTWkiPg9Ki51R6Q3_jv5v_pJbg2ShdIRg9tVLklByaXfDtdjjAvCwa1psswisQdBPsBJGDHdmpTk66_7PbYRaZOMDInQIn7wkgXRGk0A2N8Wend4Blsv9sWksTzxFdCG4L5d-5lDFMCJhg5jQFtScXiXsvtX7oZjtXvG8YjOyUtPcQKDVIrbc4CHwnxX7oZjtXAJm3T4cogRt&priceTId=2147bf1417330594171471120e1c37&skuId=4728500507602&utparam=%7B%22aplus_abtest%22%3A%22393a367e773d30f2efb16c37eb731cdc%22%7D&xxc=taobaoSearch) | 2          |
| M2螺母（雷达（螺丝M2 * 16mm）、OLED（M2 * 6mm））            | 4          |
| [M3螺母（电池仓：配螺丝M3 *16mm）](https://detail.tmall.com/item.htm?abbucket=20&id=20955552239&ns=1&priceTId=2147bf1417330591963328628e1c37&skuId=5664372939205&utparam=%7B%22aplus_abtest%22%3A%22a60ddedbdd5134dd57e79c5ed09c8c26%22%7D&xxc=taobaoSearch) | 4          |

> 小部件的统计可能会有些错误，铜柱、螺丝、螺母可以买套装的，数量可以多一些，这样避免缺少的情况；

------

## 工具准备：

1.内六角套装、2.尖嘴钳子、3.剥线钳、4.螺丝刀和可更换螺丝刀套装

其他的工具可以根据自己的需求来选择

![工具](/assets/images/工具.jpg)

------

## 底层板部分安装

> 物料准备：
>
> | 部件                                                         | 数量 |
> | :----------------------------------------------------------- | ---- |
> | 亚克力底层板                                                 | 1    |
> | 轮趣MG513P30电机（GMR编码器or霍尔编码器电机）                | 3    |
> | 轮趣C30D(ROS主控板)                                          | 1    |
> | 轮趣omni B60全向轮（安装孔径选择6mm）                        | 3    |
> | 3D打印的电机支架                                             | 3    |
> | 双通道铜柱（底板与中板支撑）：M3 * 40mm                      | 4    |
> | 双通道铜柱（固定C30D）：M3 * 10mm(这个固定C30D的铜柱，轮趣一般都会有送相关配件的) | 4    |
> | 螺丝（固定电机和电机支架）：M3 *10mm（十字槽沉头）           | 约21 |
> | 螺丝（连接铜柱）：M3 * 6mm                                   | 约8  |
> | 螺丝（固定C30D的铜柱）M3 *5mm（跟固定C30D的铜柱一样，都会有配套的） | 4    |
>
> ![微信图片_20241202182421](/assets/images/底层部件.jpg)

### 1.电机部分的安装

1.安装电机，先把电机线接好，然后需要把电机和支架的反向对正，接着将电机的螺纹孔与电机安装孔垂直对齐![微信图片_20241130232926](/assets/images/电机.jpg)![电机方向1](/assets/images/电机方向1.jpg)

**使用3个 M3 * 10 mm 螺丝（十字螺丝平头）**将电机固定到安装座上，对三个电机重复此过程。注意如果螺丝太长，会导致电机卡死，所以螺丝的总长大概10mm左右刚刚好，如果有卡死现象换成8mm左右的螺丝即可![电机方向](/assets/images/电机与支架方向.jpg)

安装完电机座后，把全向轮安装到电机输出轴上，首先把轮子上法兰盘的孔径与电机输出轴对齐，然后再拧紧螺丝即可![电机方向](/assets/images/电机方向.jpg)![拧电机](/assets/images/拧电机.jpg)

### 2.支撑铜柱的安装与C30D的接线

1.安装铜柱和电机支架，首先把**4个铜柱M3 * 40mm（底层与中层的支撑铜柱）**和**4个铜柱M3 * 10mm(固定c30d的支撑铜柱)**安装在底板上，使用**8个M3 * 6mm的螺丝**固定铜柱与底板的连接；![底层铜柱准备](/assets/images/底层铜柱准备.jpg)![底层背面](/assets/images/底层背面.jpg)![底层板安装好铜柱](/assets/images/底层板安装好铜柱.jpg)

2.注意蓝牙模块的位置STlink的接线，**白-3.3v   蓝 -Gnd   紫-SWCLK   绿-SWDIO**![蓝牙模块的安装](/assets/images/蓝牙模块的安装.jpg)![stlink的接线对应](/assets/images/stlink的接线对应.jpg)![STlink对应的接线01](/assets/images/STlink对应的接线01.jpg)

### 3.电机座与底层板的连接

1.接着把刚刚安装好的电机支架与底层板连接，使用**12个M3*10mm(十字螺丝平头)螺丝**连接3个电机支架和底板，因为电机支架是3D打印的，电机支架的螺丝孔会比较紧，需要用点力打螺丝；![把电机安装到底层板上](/assets/images/把电机安装到底层板上.jpg)![电机安装孔位](/assets/images/电机安装孔位.jpg)![把线接到电机上](/assets/images/把线接到电机上.jpg)

把C30D控制板安装到底板上的固定C30D的铜柱上，需要用轮趣提供的螺丝给板子拧紧，或者使用M3*2mm的螺丝（根据实际情况来做调整）![安装C30D](/assets/images/安装C30D.jpg)

2.然后把电机的线连接到控制板上，接线顺序要注意，将编号为Motor A（后）、Motor B（右）和Motor C（左），连接到板子上对应的Motor A（后）、Motor B（右）和Motor C（左）![电机与板子的连线](/assets/images/电机与板子的连线.jpg)

自此，底部的安装到此结束，注意先不要安装板子的电源线，这需要和中层板一块操作。![底层完工](/assets/images/底层完工.jpg)

小车已经初见雏形了，还需要安装中层板和顶层板，继续动起手来操作吧

------

## 中层板部分安装

> 物料准备：
>
> | 部件                                                         | 数量（个） |
> | ------------------------------------------------------------ | ---------- |
> | 亚克力中层板                                                 | 1          |
> | 上位机（树莓派4b或5）                                        | 1          |
> | 12V电池                                                      | 1          |
> | 3D打印电池仓                                                 | 2          |
> | DC供电线                                                     | 1          |
> | OLED的延长线：杜邦线2.54  21cm                               | 6          |
> | 双通道铜柱（中板与顶板支撑）：M3*60mm                        | 4          |
> | 双通道铜柱（固定树莓派）：M3*10mm                            | 4          |
> | [转接铜柱（单通道）：M3*4+3(内螺纹2.5)](https://item.taobao.com/item.htm?_u=1209sl7oamb1f6&id=676872916227&spm=a1z09.2.0.0.44482e8dZVD6Cx&skuId=5038903783857) | 4          |
> | 螺丝（固定树莓派转接铜柱）：M2.5 *5mm（十字槽沉头）          | 4          |
> | 螺丝  (固定电池仓)：M3 * 16mm                                | 4          |
> | 螺丝（连接铜柱）:M3 * 6mm                                    | 约12       |
> | [螺母（配螺丝M3 *16mm）：M3](https://detail.tmall.com/item.htm?abbucket=20&id=20955552239&ns=1&priceTId=2147bf1417330591963328628e1c37&skuId=5664372939205&utparam=%7B%22aplus_abtest%22%3A%22a60ddedbdd5134dd57e79c5ed09c8c26%22%7D&xxc=taobaoSearch) | 4          |
>
> ![中层的零部件准备](/assets/images/中层的零部件准备.jpg)

### 1.安装中层板支撑铜柱和电池仓

1.首先把支撑铜柱安装到中层板上，<u>**注意安装的孔位置**</u>![中层板孔位](/assets/images/中层板孔位.jpg)

使用**4个铜柱M3 * 60mm**和**8个螺丝M3 * 6mm**（固定铜柱）；随后把电池仓安装到电池仓孔位，使用**4个M3  * 16mm的螺丝**和**4个M3的螺母**； ![中层电池仓以及铜柱安装](/assets/images/中层电池仓以及铜柱安装.jpg)![中层电池仓以及铜柱安装背面](/assets/images/中层电池仓以及铜柱安装背面.jpg)

### 2.连接底板和中层板

1.先把杜邦线连接到C30D控制板的OLED位置上，然后把杜邦线从下往上穿过中层板中间的过线孔，需要注意：OLED延长杜邦线需要区分好连接C30D控制板的引脚，最好拿个标签区分好杜邦线的接线，这样不会容易搞混；

原本这个OLED是直插在C30D板子上的，所以我们只需要按照对应的引脚进行插入杜邦线即可，C30D的OLED引脚对应（从左往右）；**G->GND  3V3->VCC  D14->SCL  D13->SDA  D12->RES  D11->DC    **

![OLED对应](/assets/images/OLED对应.jpg)![oled的延长线](/assets/images/oled的延长线.jpg)

接着把供电线从上往下穿过过线孔，然后用一字螺丝到固定供电线正负极

注意**正负极**不要接反了![注意电源正负](/assets/images/注意电源正负.jpg)![中层与底层连接](/assets/images/中层与底层连接.jpg)![中层与底层连接01](/assets/images/中层与底层连接01.jpg)

2.固定底层支撑铜柱，使用4个**M3 * 6mm螺丝**连接,注意安装孔位![中层与底层连接02](/assets/images/中层与底层连接02.jpg)

### 3.树莓派和电池安装

1.因为中层板的树莓派孔位是M3的孔，但是树莓派的螺丝孔又是M2.5的，所以我们需要用到铜柱转接，把固定树莓派的转接铜柱安装到指定的孔位，使用**4个转接铜柱（内螺纹2.5）**然后用**4个M2.5 * 5mm（十字平头）的螺丝**锁紧![树莓派转接铜柱](/assets/images/树莓派转接铜柱.jpg)

这里可以先把M2.5的螺丝放进树莓派之后，再去拧螺丝会比较轻松![树莓派的安装](/assets/images/树莓派的安装.jpg)

2.然后把12V电池放在电池仓内，连接供电线；中层部分的安装就到此结束了![中层完工](/assets/images/中层完工.jpg)![中层完工01](/assets/images/中层完工01.jpg)

现在还差最后的顶层安装，坚持就是胜利

------

## 顶层板部分安装

> 物料准备：
>
> | 部件                                                         | 数量（个） |
> | ------------------------------------------------------------ | ---------- |
> | 亚克力顶层板                                                 | 1          |
> | N10P雷达                                                     | 1          |
> | N10P雷达串口转接板                                           | 1          |
> | 3D打印雷达支撑件                                             | 1          |
> | OLED屏( C30D控制板)                                          | 1          |
> | 双通道铜柱（雷达支撑）：M3 *30mm                             | 4          |
> | 双通道铜柱（OLED支架固定）：M3 *10mm                         | 2          |
> | 双通道铜柱（固定雷达串口转接板）：M2 * 10mm                  | 4          |
> | [内六角螺丝（雷达固定，螺丝头部直径3.8mm左右）：M2*16mm](https://detail.tmall.com/item.htm?abbucket=20&id=635755541429&ns=1&pisk=fKWSKQ0Tw405FUPz1DE2lWSCQRvCRwwZPDtdjMHrvLpJJssGRUr3ZL5XRZQXyYruZBLCrLdhae8yRpsh5ozaQRSlqpA87PyatnbUdd0-2Y3EHIK6ZrrquRSlqpmSJl5YQ2ZcJwDK9eQpHIKBjpKJ2bLYcHt6JpLJ9qhvXEppJwLpkEKev3KppQEjMHKsybKJ2npvjHoJppQdDvFrfHNWrgZVLePLcRV5fEMKCcx9w7jSTvDhN3d5Qi8X0nWXVQT6gJ9OZTQVvTWkiPg9Ki51R6Q3_jv5v_pJbg2ShdIRg9tVLklByaXfDtdjjAvCwa1psswisQdBPsBJGDHdmpTk66_7PbYRaZOMDInQIn7wkgXRGk0A2N8Wend4Blsv9sWksTzxFdCG4L5d-5lDFMCJhg5jQFtScXiXsvtX7oZjtXvG8YjOyUtPcQKDVIrbc4CHwnxX7oZjtXAJm3T4cogRt&priceTId=2147bf1417330594171471120e1c37&skuId=4728500507602&utparam=%7B%22aplus_abtest%22%3A%22393a367e773d30f2efb16c37eb731cdc%22%7D&xxc=taobaoSearch) | 2          |
> | 螺丝（OLED连接支架）：M2*6mm                                 | 2          |
> | 螺丝（固定雷达串口转接板）：M2 *5mm                          | 8          |
> | 螺丝（连接铜柱（雷达8个、OLED4个、顶层与中层连接4个））：M3 * 6mm（十字槽沉头） | 约16       |
> | M2螺母（雷达、OLED）                                         | 4          |
> 
>![上层板物料准备](/assets/images/上层板物料准备.jpg)

### 1.安装雷达和OLED支撑铜柱的安装

1.准备**4个M3 * 30mm的铜柱（雷达支撑）**、**2个M3 * 6mm的铜柱（固定OLED）**和**4个M3 * 8mm的铜柱（雷达串口转接板）**，按照对应的孔位进行安装![顶层板孔位](/assets/images/顶层板孔位.jpg)![顶层孔位安装01](/assets/images/顶层孔位安装01.jpg)

### 2.安装雷达串口转接板

1.使用8个M2*5mm的螺丝和4个M2铜柱，把雷达串口板安装到对应的孔位![雷达串口转接板安装01](/assets/images/雷达串口转接板安装01.jpg)![雷达串口转接板安装](/assets/images/雷达串口转接板安装.jpg)

### 3.安装雷达

1.安装雷达，首先先把3D打印的雷达支撑件安装到刚刚装好的雷达支撑铜柱上，注意方向，随后准备**2个M2 * 16mm的内六角螺丝**（装雷达与打印件连接）和**M2螺母**，把M2的螺母塞进3D打印的雷达支撑件里，用点小技巧把螺母拧到螺丝上，然后用螺丝给它下压压下去![雷达安装螺母](/assets/images/雷达安装螺母.jpg)

2.把**2个M2 * 16 mm的内六角螺丝**穿进雷达的俩个孔中，需要注意的是，雷达的俩个孔可能会小了一些，可以先螺丝反过来，然后塞进雷达的螺丝孔，左右摆动扩大孔位（刚刚好就行），**小心不要伤到雷达了**，当然也可以用别的方法来解决![微信图片_20241202191921](/assets/images/雷达安装.jpg)![微信图片编辑_20241202183818](/assets/images/雷达安装2.jpg)

3.把螺丝穿过雷达孔后就把雷达放到雷达支撑架上，注意雷达的摆放方向，然后用1.5的内六角把螺丝给拧紧

![微信图片编辑_20241202193947](/assets/images/雷达安装3.jpg)![微信图片_20241202193337](/assets/images/雷达安装4.jpg)

### 4.安装OLED

1.先把安装OLED的工具准备好![OLED安装](/assets/images/OLED安装.jpg)

2.把M2 * 6mm的螺丝穿过OLED的螺丝孔位，然后上M2的螺母，这里螺丝上2个即可，不需要把4个螺丝孔都上螺丝![OLED安装01](/assets/images/OLED安装01.jpg)**<u>拧螺丝的时候一定要注意螺丝的头，不然会把OLED屏幕搞碎</u>**，随后把OLED支架装上去，***这里装配的时候需要俩边对称拧***，这是因为怕把OLED搞坏了（OLED太容易碎了）![OLED安装02](/assets/images/OLED安装02.jpg)![OLED安装03](/assets/images/OLED安装03.jpg)

3.安装完OLED支架部分后，就把OLED安装到顶层板的OLED固定孔位上,需要用到**2个M3 *6mm的螺丝**![OLED安装到顶层板](/assets/images/OLED安装到顶层板.jpg)

顶层部分就已经完成了，现在还需要拼接起来![顶层板完工](/assets/images/顶层板完工.jpg)

### 5.连接中层板和顶层板

1.将杜邦线穿过OLED的过线孔，然后与OLED连接上（注意OLED对应C30D的母座），用**4个M3 * 6mm的螺丝**固定顶层与中层支撑铜柱的连接，注意安装的孔位，实际安装时铜柱可能会有些偏，需要手扶着中层板的支撑铜柱进行安装![顶层与中层连接孔位](/assets/images/顶层与中层连接孔位.jpg)![顶层与中层连接](/assets/images/顶层与中层连接.jpg)到这步就已经把小车的顶部安装完成了![总装](/assets/images/总装.jpg)![总装01](/assets/images/总装01.jpg)

好啦，小车的底、中、顶三层部分都已经安装完成了，已经像个像样的Omni小车了，不过还差最后一部分，就是上下位机的连线

------

## 小车的上下位机连线

物料准备：

> | 部件                                                         | 数量 |
> | ------------------------------------------------------------ | ---- |
> | 双头type-c的线（C30D控制板给树莓派供电）                     | 1    |
> | USB转type-c的线（C30D与树莓派通讯，雷达串口转接板与树莓派连接） | 2    |

双头type-c线的长度大概在20CM左右，当然也可以长一些；USB转Type-c的线大概30CM左右，线太长不容易整理线的布局，根据图中的标识来接线即可；

注意板子的接口作用，不要接错线了

![C30D功能](/assets/images/C30D功能.jpg)![C30Dtype-c](/assets/images/C30Dtype-c.jpg)![微信图片_20241202205149](/assets/images/c30d板子type-c.jpg)<img src="/assets/images/树莓派接口说明.jpg" alt="树莓派接口说明" style="zoom:33%;" />

把程序烧录进去之后，转动电位器改变小车模式

![微信图片编辑_20241202210606](/assets/images/调节电位器.jpg)![微信图片编辑_20241202210606](/assets/images/全向轮模式.png)

需要把电机的使能开关开起来电机才能动![电机使能](/assets/images/电机使能.jpg)注意C30D控制板，不要有任何可以导电的材质在板子内或者贴着控制板，这会导致内部短路，但板子内有电路保护的功能，板子会冒出红灯警告![注意短路](/assets/images/注意短路.jpg)

到此一台完整的Omni全向轮小车就搭建完成，接下来就进入软件方面学习吧

