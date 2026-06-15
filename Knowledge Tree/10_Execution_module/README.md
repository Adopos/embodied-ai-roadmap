# 10_执行模块

## 1. 模块定位

执行模块负责让具身智能体的“身体”真正行动起来。

它回答的问题是：

> 智能体已经产生了控制指令之后，如何让真实硬件或仿真身体执行动作？

执行模块不是负责“思考”的模块，也不是负责“规划路径”的模块。
它主要负责底层硬件、执行器、传感器接口、通信系统和机器人身体运动。

一句话概括：

> 执行模块负责“把控制指令变成真实或仿真的身体动作”。

在完整具身智能体中，执行模块通常位于控制模块之后、外部环境之前：

```text id="whuv75"
控制模块
  ↓
执行模块
  ↓
真实机器人 / 仿真机器人
  ↓
外部环境
```

---

## 2. 模块输入

执行模块可能接收以下输入：

```text id="3hbk8s"
电机控制指令
舵机角度指令
轮速指令
底盘速度指令
机械臂关节指令
夹爪开合指令
无人机飞控指令
传感器读取指令
上位机发送的控制命令
ROS 2 节点发送的执行命令
```

例子：

```text id="lgt9lp"
左轮速度：0.5 m/s
右轮速度：0.5 m/s
舵机角度：90°
机械臂关节角：[30°, 45°, 20°]
夹爪状态：close
无人机目标高度：2 m
```

---

## 3. 模块输出

执行模块的输出是真实或仿真环境中的动作和传感器反馈。

常见输出：

```text id="cp1ff8"
电机转动
舵机转动
轮子运动
底盘移动
机械臂运动
夹爪开合
无人机飞行
传感器采样数据
执行状态反馈
硬件异常信息
```

例子：

```json id="j32c3r"
{
  "actuator": "left_motor",
  "status": "running",
  "target_speed": 0.5,
  "actual_speed": 0.48
}
```

或者：

```json id="a4hjf2"
{
  "sensor": "imu",
  "roll": 0.02,
  "pitch": -0.01,
  "yaw": 1.57
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 嵌入式系统

作用：

> 理解微控制器、外设、中断、定时器、通信和实时控制，是机器人底层执行系统的基础。

推荐书籍：

* Jonathan W. Valvano：《Embedded Systems: Introduction to ARM Cortex-M Microcontrollers》
* Edward A. Lee, Sanjit A. Seshia：《Introduction to Embedded Systems》
* David E. Simon：《An Embedded Software Primer》

推荐教程 / 网课：

* UT Austin Embedded Systems 相关课程
* Coursera / edX Embedded Systems 课程
* ARM Cortex-M 官方资料
* STM32 官方入门教程
* 嵌入式系统公开课

对应项目：

* 嵌入式点灯实验
* 定时器控制实验
* 外设驱动实验
* 传感器读取实验
* 电机控制实验
* 机器人下位机控制系统

---

### 4.2 STM32 开发

作用：

> 使用 STM32 作为机器人下位机，完成传感器读取、电机控制、通信和实时控制任务。

推荐书籍：

* Joseph Yiu：《The Definitive Guide to ARM Cortex-M3 and Cortex-M4 Processors》
* Jonathan W. Valvano：《Embedded Systems: Real-Time Interfacing to ARM Cortex-M Microcontrollers》
* STM32 官方参考手册和数据手册

推荐教程 / 网课：

* ST 官方 STM32 Step-by-Step
* ST STM32CubeMX / STM32CubeIDE 官方教程
* 江科大 STM32 教程
* 正点原子 STM32 教程
* 野火 STM32 教程

对应项目：

* STM32 点灯
* STM32 串口通信
* STM32 PWM 输出
* STM32 读取传感器
* STM32 控制舵机
* STM32 控制编码器电机
* STM32 小车底盘控制

---

### 4.3 单片机原理

作用：

> 理解单片机内部结构、外设资源、寄存器、存储器、中断和基本控制流程。

推荐书籍：

* Jonathan W. Valvano：《Embedded Systems: Introduction to ARM Cortex-M Microcontrollers》
* Kenneth J. Ayala：《The 8051 Microcontroller》
* Mazidi：《The 8051 Microcontroller and Embedded Systems》

推荐教程 / 网课：

* 51 单片机系统教程
* STM32 单片机系统教程
* 中国大学 MOOC 单片机原理课程
* B站单片机原理课程
* Keil / STM32CubeIDE 入门教程

对应项目：

* GPIO 输入输出实验
* 按键控制 LED
* 定时器中断实验
* 串口收发实验
* ADC 采样实验
* 简单传感器读取实验

---

### 4.4 电路基础

作用：

> 理解电压、电流、电阻、电源、信号、电机驱动和传感器接线，是做真实机器人硬件的基础。

推荐书籍：

* Charles K. Alexander, Matthew N. O. Sadiku：《Fundamentals of Electric Circuits》
* James W. Nilsson, Susan Riedel：《Electric Circuits》
* Paul Horowitz, Winfield Hill：《The Art of Electronics》

推荐教程 / 网课：

* MIT OCW Circuits and Electronics
* 中国大学 MOOC 电路原理课程
* B站电路基础课程
* All About Circuits 教程
* Arduino / STM32 电路连接教程

对应项目：

* LED 限流电路
* 按键输入电路
* 传感器接线
* 电机驱动接线
* 电源供电测试
* 机器人电源分配实验

---

### 4.5 模拟电子技术

作用：

> 理解放大、滤波、运放、模拟信号采集和传感器信号调理。

推荐书籍：

* Adel S. Sedra, Kenneth C. Smith：《Microelectronic Circuits》
* Paul Horowitz, Winfield Hill：《The Art of Electronics》
* Thomas L. Floyd：《Electronic Devices》

推荐教程 / 网课：

* MIT OCW Circuits and Electronics
* 中国大学 MOOC 模拟电子技术课程
* B站模电系统课程
* Analog Devices 教程
* TI Precision Labs

对应项目：

* 传感器模拟信号采集
* ADC 采样实验
* 简单滤波电路
* 运放放大电路
* 电压采样电路
* 电池电压检测电路

---

### 4.6 数字电子技术

作用：

> 理解数字逻辑、时序电路、接口电路和数字系统，是单片机、通信和嵌入式系统的基础。

推荐书籍：

* M. Morris Mano, Michael Ciletti：《Digital Design》
* Thomas L. Floyd：《Digital Fundamentals》
* John F. Wakerly：《Digital Design: Principles and Practices》

推荐教程 / 网课：

* MIT OCW Computation Structures
* 中国大学 MOOC 数字电子技术课程
* B站数电系统课程
* FPGA / Verilog 入门教程
* 数字逻辑与计算机组成课程

对应项目：

* 按键消抖实验
* 数码管显示
* 编码器信号读取
* 简单逻辑控制电路
* SPI / I2C 数字通信理解
* FPGA / Verilog 入门实验

---

### 4.7 电机与驱动系统

作用：

> 理解机器人常用执行器和驱动方式，包括直流电机、步进电机、舵机、无刷电机和电机驱动器。

推荐书籍：

* Austin Hughes, Bill Drury：《Electric Motors and Drives》
* R. Krishnan：《Electric Motor Drives: Modeling, Analysis, and Control》
* Ned Mohan：《Electric Machines and Drives》

推荐教程 / 网课：

* ST Motor Control 官方教程
* Texas Instruments Motor Control 教程
* MATLAB / Simulink Motor Control 教程
* STM32 电机控制教程
* 电机拖动与电机控制课程

对应项目：

* 直流电机驱动
* 编码器电机驱动
* 舵机控制
* 步进电机控制
* 无刷电机入门
* 小车底盘电机驱动系统
* 机械臂关节驱动实验

---

### 4.8 传感器与执行器接口

作用：

> 连接传感器、执行器和控制板，让机器人能够感知环境并驱动身体运动。

推荐书籍：

* Jacob Fraden：《Handbook of Modern Sensors》
* John Vetelino, Aravind Reghu：《Introduction to Sensors》
* Clarence W. de Silva：《Sensors and Actuators: Engineering System Instrumentation》

推荐教程 / 网课：

* Arduino 传感器教程
* STM32 传感器教程
* Raspberry Pi 传感器教程
* Intel RealSense 官方文档
* RPLIDAR / Livox / Velodyne 官方文档

对应项目：

* 超声波测距
* 红外避障
* IMU 姿态读取
* 编码器读取
* 摄像头读取
* LiDAR 数据读取
* 舵机 / 电机执行器控制

---

### 4.9 通信协议与接口

作用：

> 让上位机、下位机、传感器、执行器和机器人软件系统之间交换数据。

推荐书籍：

* Jan Axelson：《Serial Port Complete》
* Jan Axelson：《USB Complete》
* Wilfried Voss：《A Comprehensible Guide to Controller Area Network》

推荐教程 / 网课：

* UART / I2C / SPI / CAN 教程
* STM32 通信协议教程
* ROS 2 通信教程
* MAVLink 官方文档
* WebSocket / MQTT 教程

对应项目：

* UART 串口通信
* I2C 读取传感器
* SPI 读取设备
* CAN 总线通信
* USB 串口通信
* 上位机向下位机发送控制命令
* ROS 2 与 STM32 通信

---

### 4.10 机器人硬件系统

作用：

> 从整体角度理解机器人由哪些硬件组成，以及这些硬件如何组合成一个可运行系统。

推荐书籍：

* John J. Craig：《Introduction to Robotics: Mechanics and Control》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》
* Bruno Siciliano 等：《Robotics: Modelling, Planning and Control》

推荐教程 / 网课：

* 机器人系统设计课程
* 移动机器人制作教程
* TurtleBot3 官方教程
* ROS 2 机器人硬件接入教程
* 机器人底盘 / 机械臂 DIY 教程

对应项目：

* 两轮差速小车
* 四轮小车
* 简单机械臂
* 视觉小车
* ROS 2 移动机器人
* 机器人底盘硬件系统
* 具身智能实验平台原型

---

### 4.11 机械设计基础

作用：

> 理解机器人结构、连接件、传动方式、材料和装配，是从仿真走向真实机器人的必要基础。

推荐书籍：

* Robert L. Norton：《Machine Design: An Integrated Approach》
* Shigley：《Mechanical Engineering Design》
* Robert L. Mott：《Machine Elements in Mechanical Design》

推荐教程 / 网课：

* SolidWorks 官方教程
* Fusion 360 官方教程
* 机械设计基础课程
* 3D 打印结构设计教程
* 机器人结构设计教程

对应项目：

* 小车底盘结构设计
* 传感器安装支架设计
* 机械臂简单结构设计
* 3D 打印机器人外壳
* 轮式机器人结构优化
* 陆空变形机器人结构概念设计

---

### 4.12 机器人操作系统 ROS 2

作用：

> 将机器人传感器、执行器、控制、规划、导航和上位机系统连接成完整软件架构。

推荐书籍：

* Francisco Martín Rico：《A Concise Introduction to Robot Programming with ROS2》
* Lentin Joseph：《Robot Operating System for Absolute Beginners》
* Morgan Quigley, Brian Gerkey, William D. Smart：《Programming Robots with ROS》

推荐教程 / 网课：

* ROS 2 官方 Tutorials
* The Construct ROS 2 课程
* 古月居 ROS 2 教程
* TurtleBot3 ROS 2 教程
* ROS 2 Control 官方文档

对应项目：

* ROS 2 基础节点
* ROS 2 Topic 通信
* ROS 2 Service 通信
* ROS 2 Action 通信
* ROS 2 控制机器人底盘
* ROS 2 接入传感器数据
* ROS 2 + STM32 小车系统

---

### 4.13 上位机 / 下位机系统

作用：

> 建立 AI 决策层、机器人软件层和硬件控制层之间的分工与通信。

推荐书籍：

* David E. Simon：《An Embedded Software Primer》
* Lentin Joseph：《Robot Operating System for Absolute Beginners》
* Martin Fowler：《Patterns of Enterprise Application Architecture》

推荐教程 / 网课：

* ROS 2 + STM32 通信教程
* 上位机控制下位机教程
* Python 串口通信教程
* C# / Qt 上位机开发教程
* 串口助手与协议设计教程

对应项目：

* Python 上位机发送串口命令
* STM32 下位机解析控制指令
* 上位机显示传感器数据
* 上位机控制小车前进、后退、转向
* ROS 2 上位机 + STM32 下位机机器人系统

---

### 4.14 边缘计算与机器人计算平台

作用：

> 理解机器人上运行 AI、视觉、规划和控制所需的计算平台，例如 Raspberry Pi、Jetson、工控机和 MCU。

推荐书籍：

* Derek Molloy：《Exploring Raspberry Pi》
* Donald Norris：《Raspberry Pi Projects for the Evil Genius》
* NVIDIA Jetson 官方开发文档

推荐教程 / 网课：

* Raspberry Pi 官方文档
* NVIDIA Jetson Developer Resources
* JetPack SDK 官方教程
* Jetson AI / Robotics 教程
* 边缘 AI 部署教程

对应项目：

* Raspberry Pi 读取摄像头
* Raspberry Pi 控制小车
* Jetson 运行 YOLO
* Jetson 接入 ROS 2
* Jetson + STM32 机器人系统
* 边缘端运行视觉模型并控制机器人

---

## 5. 项目验证

### 5.1 入门项目：STM32 点灯与按键输入

目标：

```text id="yaul5k"
完成最基础的单片机输入输出控制。
```

功能：

```text id="rhroy0"
GPIO 输出
GPIO 输入
按键检测
LED 状态切换
```

验证能力：

```text id="wujia3"
能搭建 STM32 开发环境
能下载程序到开发板
能理解基本输入输出
```

---

### 5.2 入门项目：STM32 串口通信

目标：

```text id="1gm3zt"
实现 STM32 与电脑之间的数据收发。
```

功能：

```text id="cp8y26"
串口发送数据
串口接收数据
打印传感器状态
接收上位机命令
```

验证能力：

```text id="ideq6i"
能让下位机和上位机通信
能为后续机器人控制协议打基础
```

---

### 5.3 入门项目：传感器读取

目标：

```text id="gd2aqs"
读取机器人常用传感器数据。
```

可选传感器：

```text id="e7hb17"
超声波
红外避障
IMU
编码器
电池电压
摄像头
LiDAR
```

验证能力：

```text id="dci8as"
能获取真实环境或机器人自身信息
能把传感器数据传给状态与感知模块
```

---

### 5.4 进阶项目：舵机与电机控制

目标：

```text id="jzga2t"
让执行器按照控制指令运动。
```

功能：

```text id="ec9xg2"
PWM 控制舵机
驱动直流电机
控制步进电机
读取编码器反馈
调节电机速度
```

验证能力：

```text id="wgns0b"
能让机器人身体产生真实动作
能理解执行器和控制指令之间的关系
```

---

### 5.5 进阶项目：STM32 小车底盘

目标：

```text id="bfoffh"
搭建一个可以运动的小车底盘。
```

功能：

```text id="asudvj"
前进
后退
左转
右转
原地旋转
停止
速度调节
```

验证能力：

```text id="r10n67"
能完成真实移动机器人底层执行系统
能把控制模块输出转化为真实底盘运动
```

---

### 5.6 进阶项目：上位机控制下位机

目标：

```text id="qwcb03"
通过电脑或上位机程序控制 STM32 下位机执行动作。
```

功能：

```text id="s9jx3f"
上位机发送控制命令
下位机解析命令
下位机控制电机或舵机
下位机返回状态
上位机显示状态
```

验证能力：

```text id="qtl46m"
能建立机器人系统的上下层架构
能让 AI / ROS / 控制程序和硬件系统连接起来
```

---

### 5.7 高级项目：ROS 2 + STM32 小车

目标：

```text id="kyvx8t"
将 ROS 2 上位机系统和 STM32 底层控制系统连接起来。
```

功能：

```text id="e9qabq"
ROS 2 发布速度指令
STM32 接收控制命令
STM32 控制电机
STM32 返回编码器数据
ROS 2 接收底盘状态
```

验证能力：

```text id="x926uw"
能把机器人软件系统和真实硬件系统打通
能为 SLAM、导航、控制和具身智能项目打基础
```

---

### 5.8 高级项目：边缘 AI 机器人执行平台

目标：

```text id="9pi4kc"
使用 Raspberry Pi / Jetson 运行视觉或 AI 模型，并控制下位机执行动作。
```

功能：

```text id="4qvxa9"
摄像头采集图像
边缘设备运行视觉模型
识别目标或障碍物
发送控制命令给 STM32
STM32 控制电机或舵机
```

验证能力：

```text id="15048g"
能将 AI 感知、上位机计算和底层执行连接起来
能形成具身智能体的基础硬件闭环
```

---

### 5.9 高级项目：完整机器人硬件执行系统

目标：

```text id="2ezti1"
搭建一个具备传感器、执行器、上位机、下位机和电源系统的完整机器人执行平台。
```

组成：

```text id="7ng0w4"
主控计算平台
下位机控制板
电机驱动
执行器
传感器
电池和电源模块
通信模块
机械结构
```

验证能力：

```text id="tamdty"
能从系统层面搭建机器人硬件平台
能支撑后续感知、状态、规划、控制、学习等模块接入
```

---

## 6. 学习状态记录

| 知识点           | 当前状态 |
| ------------- | ---- |
| 嵌入式系统         | 未开始  |
| STM32 开发      | 入门   |
| 单片机原理         | 了解   |
| 电路基础          | 了解   |
| 模拟电子技术        | 未开始  |
| 数字电子技术        | 入门   |
| 电机与驱动系统       | 了解   |
| 传感器与执行器接口     | 了解   |
| 通信协议与接口       | 未开始  |
| 机器人硬件系统       | 未开始  |
| 机械设计基础        | 未开始  |
| 机器人操作系统 ROS 2 | 未开始  |
| 上位机 / 下位机系统   | 未开始  |
| 边缘计算与机器人计算平台  | 了解   |

状态标准：

```text id="w7hivq"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

执行模块最终要实现：

```text id="u7u5jd"
智能体能够控制真实或仿真的机器人身体；
能够读取传感器数据；
能够驱动电机、舵机、机械臂、夹爪或无人机执行器；
能够实现上位机与下位机通信；
能够把 ROS 2、AI 模型、控制算法和底层硬件连接起来；
能够形成真实机器人系统的基础执行闭环。
```

最终效果：

> 智能体不只是停留在算法和仿真中，而是能够通过真实硬件产生动作，并与真实环境发生交互。

