# 09_控制模块

## 1. 模块定位

控制模块负责把规划模块输出的路径、轨迹或目标状态，转化为机器人可以稳定执行的控制指令。

它回答的问题是：

> 智能体已经知道要怎么走、怎么动之后，如何让身体稳定、准确地执行？

控制模块不负责决定任务目标，也不负责生成路径。
它主要负责让机器人按照目标速度、目标位置、目标姿态或目标轨迹运动。

一句话概括：

> 控制模块负责“把规划结果稳定、准确地执行出来”。

在完整具身智能体中，控制模块通常位于规划模块之后、执行模块之前：

```text id="y1wbyl"
规划模块
  ↓
控制模块
  ↓
执行模块
  ↓
真实机器人 / 仿真机器人
```

---

## 2. 模块输入

控制模块可能接收以下输入：

```text id="4ed6l3"
目标位置
目标速度
目标姿态
目标轨迹
目标关节角
目标末端位姿
当前机器人状态
当前速度
当前姿态
当前关节角
当前传感器反馈
机器人动力学约束
安全约束
规划模块输出的路径或轨迹
```

例子：

```text id="d5plxu"
目标速度：0.5 m/s
目标角速度：0.2 rad/s
目标位置：[2.0, 1.5]
目标姿态：保持水平
目标关节角：[30°, 45°, 20°]
当前速度：0.3 m/s
当前偏差：向左偏离 0.2 m
```

---

## 3. 模块输出

控制模块的输出是可以交给执行模块或底层驱动系统的控制指令。

常见输出：

```text id="os0j6m"
底盘线速度
底盘角速度
左右轮目标速度
电机控制量
舵机角度
关节角度
关节速度
关节力矩
无人机姿态控制量
无人机高度控制量
轨迹跟踪修正量
```

例子：

```json id="hmgj37"
{
  "control_type": "mobile_base",
  "linear_velocity": 0.5,
  "angular_velocity": 0.2
}
```

或者：

```json id="7beg1h"
{
  "control_type": "robot_arm",
  "joint_targets": [30, 45, 20, 10],
  "control_mode": "position_control"
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 自动控制原理

作用：

> 建立反馈控制、系统稳定性、动态响应和误差调节的基础，是控制模块最核心的底层知识。

推荐书籍：

* Katsuhiko Ogata：《Modern Control Engineering》
* Norman S. Nise：《Control Systems Engineering》
* Gene F. Franklin, J. David Powell, Abbas Emami-Naeini：《Feedback Control of Dynamic Systems》

推荐教程 / 网课：

* MIT OCW 6.302 Feedback Systems
* MIT OCW RES.6-010 Electronic Feedback Systems
* University of Michigan Control Tutorials for MATLAB and Simulink
* 中国大学 MOOC 自动控制原理课程
* B站自动控制原理系统课程

对应项目：

* 小车速度闭环控制
* 电机位置闭环控制
* 温度 / 距离 / 速度反馈控制实验
* 轨迹跟踪误差修正
* 简单机器人稳定控制实验

---

### 4.2 现代控制理论

作用：

> 使用状态空间方法描述和控制系统，适合处理多变量系统、机器人系统和复杂动态系统。

推荐书籍：

* Chi-Tsong Chen：《Linear System Theory and Design》
* Katsuhiko Ogata：《Modern Control Engineering》
* Richard C. Dorf, Robert H. Bishop：《Modern Control Systems》
* João P. Hespanha：《Linear Systems Theory》

推荐教程 / 网课：

* MIT OCW 16.30 Feedback Control Systems
* MIT OCW 2.14 Analysis and Design of Feedback Control Systems
* State-Space Control 系统教程
* Linear Systems and Control 相关课程

对应项目：

* 状态空间建模实验
* 小车状态反馈控制
* 倒立摆控制仿真
* LQR 小实验
* 多状态系统稳定控制仿真

---

### 4.3 机器人控制

作用：

> 研究移动机器人、机械臂和复杂机器人系统如何根据目标运动稳定执行。

推荐书籍：

* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* Bruno Siciliano 等：《Robotics: Modelling, Planning and Control》
* Mark W. Spong, Seth Hutchinson, M. Vidyasagar：《Robot Modeling and Control》

推荐教程 / 网课：

* Modern Robotics Coursera Specialization
* Northwestern Modern Robotics 官方课程资源
* 机器人控制公开课
* ROS 2 Control 官方文档
* MoveIt 2 控制相关教程

对应项目：

* 移动机器人速度控制
* 差速小车轨迹跟踪
* 机械臂关节控制
* 机械臂末端位置控制
* ROS 2 Control 控制机器人关节
* 机器人运动规划结果的跟踪控制

---

### 4.4 电机控制

作用：

> 控制直流电机、编码器电机、步进电机、无刷电机和舵机，是机器人执行动作的底层基础。

推荐书籍：

* R. Krishnan：《Electric Motor Drives: Modeling, Analysis, and Control》
* Austin Hughes, Bill Drury：《Electric Motors and Drives》
* Ned Mohan：《Electric Machines and Drives》

推荐教程 / 网课：

* ST Motor Control 官方教程
* Texas Instruments Motor Control 教程
* MATLAB / Simulink Motor Control 教程
* STM32 电机控制教程
* 电机拖动与电机控制课程

对应项目：

* 直流电机速度控制
* 编码器电机闭环控制
* 步进电机位置控制
* 舵机角度控制
* 无刷电机控制入门
* 小车底盘电机控制

---

### 4.5 运动控制

作用：

> 控制机器人按照期望速度、位置、姿态或轨迹进行运动，重点关注运动执行的准确性和平滑性。

推荐书籍：

* Katsuhiko Ogata：《Modern Control Engineering》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》

推荐教程 / 网课：

* 移动机器人运动控制课程
* Differential Drive Robot Control 教程
* ROS 2 Control 官方文档
* Navigation2 Controller Server 文档
* MATLAB Mobile Robot Control 教程

对应项目：

* 差速小车运动控制
* 小车直线行驶控制
* 小车转向控制
* 小车轨迹跟踪控制
* 机器人按路径点运动
* 移动机器人局部控制器实验

---

### 4.6 无人机控制

作用：

> 控制无人机的姿态、高度、速度和位置，是空中机器人和智能无人系统的重要基础。

推荐书籍：

* Randal W. Beard, Timothy W. McLain：《Small Unmanned Aircraft: Theory and Practice》
* Quan Quan：《Introduction to Multicopter Design and Control》
* Kimon P. Valavanis, George J. Vachtsevanos：《Handbook of Unmanned Aerial Vehicles》

推荐教程 / 网课：

* PX4 官方文档
* PX4 Multicopter Control Architecture 文档
* ArduPilot 官方文档
* MAVLink 官方文档
* 无人机控制与飞控系统课程

对应项目：

* 无人机高度控制仿真
* 无人机姿态控制仿真
* 四旋翼位置控制实验
* PX4 仿真控制实验
* AirSim 无人机控制实验
* 无人机配送任务中的飞行控制

---

### 4.7 车辆控制

作用：

> 控制轮式车辆、小车、无人车等系统的速度、转向和轨迹跟踪。

推荐书籍：

* Rajesh Rajamani：《Vehicle Dynamics and Control》
* Thomas D. Gillespie：《Fundamentals of Vehicle Dynamics》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》

推荐教程 / 网课：

* Coursera Self-Driving Cars Specialization
* Udacity Self-Driving Car Nanodegree 控制部分
* Autonomous Vehicle Control 相关课程
* PythonRobotics 车辆控制教程
* MATLAB Automated Driving Toolbox 教程

对应项目：

* 小车速度控制
* 小车转向控制
* Pure Pursuit 轨迹跟踪
* Stanley 控制实验
* 无人车路径跟踪仿真
* 电赛控制类小车项目

---

### 4.8 最优控制与模型预测控制

作用：

> 在约束条件下寻找更优控制输入，适合轨迹跟踪、无人车控制、无人机控制和机械臂控制。

推荐书籍：

* Dimitri P. Bertsekas：《Dynamic Programming and Optimal Control》
* Frank L. Lewis, Draguna Vrabie, Vassilis L. Syrmos：《Optimal Control》
* James B. Rawlings, David Q. Mayne, Moritz Diehl：《Model Predictive Control: Theory, Computation, and Design》

推荐教程 / 网课：

* MIT / Stanford Optimal Control 相关课程
* Model Predictive Control 公开课
* CasADi 官方教程
* do-mpc 官方教程
* MATLAB MPC Toolbox 教程

对应项目：

* 小车轨迹跟踪 MPC 仿真
* 无人机位置控制 MPC 仿真
* 倒立摆最优控制
* 约束条件下的速度规划与控制
* 机械臂轨迹优化控制实验

---

### 4.9 学习型控制

作用：

> 使用机器学习、强化学习或模仿学习方法学习控制策略，适合复杂模型难以精确建立的场景。

推荐书籍：

* Dimitri P. Bertsekas：《Reinforcement Learning and Optimal Control》
* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Jan Peters, Sethu Vijayakumar, Stefan Schaal 等机器人学习相关资料

推荐教程 / 网课：

* Berkeley CS285: Deep Reinforcement Learning
* David Silver Reinforcement Learning Course
* Hugging Face Deep RL Course
* Isaac Lab 控制与强化学习教程
* MuJoCo / Gymnasium 控制任务教程

对应项目：

* 倒立摆强化学习控制
* 小车速度控制策略学习
* MuJoCo 机器人控制
* Isaac Lab 机器人控制训练
* 用 RL 学习无人机或小车控制策略
* 模仿学习控制机械臂动作

---

## 5. 项目验证

### 5.1 入门项目：直流电机速度控制

目标：

```text id="g3qr71"
控制直流电机以指定速度稳定转动。
```

功能：

```text id="d7sxh9"
读取编码器速度
计算速度误差
输出控制量
调整电机速度
记录速度曲线
```

验证能力：

```text id="hvmf5t"
能理解反馈控制
能实现基础电机闭环
能分析目标速度和实际速度之间的误差
```

---

### 5.2 入门项目：舵机角度控制

目标：

```text id="c3p5dx"
控制舵机转到指定角度。
```

功能：

```text id="tki6rf"
输入目标角度
生成控制信号
舵机转动到目标位置
测试不同角度响应
```

验证能力：

```text id="wh9r2v"
能理解位置控制
能让执行器按照目标动作运行
能为机械臂和小车转向打基础
```

---

### 5.3 进阶项目：编码器电机闭环控制

目标：

```text id="hkjdej"
使用编码器反馈实现电机速度或位置闭环控制。
```

功能：

```text id="b08344"
读取编码器
计算速度或位置
与目标值比较
输出控制量
稳定跟踪目标
```

验证能力：

```text id="tpw82g"
能完成真实控制闭环
能理解反馈、误差和稳定性
能为小车底盘控制打基础
```

---

### 5.4 进阶项目：差速小车运动控制

目标：

```text id="7suoty"
控制差速小车按照指定速度和角速度运动。
```

功能：

```text id="w2hd48"
输入线速度和角速度
转换为左右轮速度
控制左右电机
实现前进、后退、转向、原地旋转
```

验证能力：

```text id="w1gqsq"
能把高层运动指令转成底层电机控制
能理解移动机器人运动控制
能为导航模块接入做准备
```

---

### 5.5 进阶项目：小车轨迹跟踪控制

目标：

```text id="lb5l53"
让小车按照规划路径或轨迹运动。
```

功能：

```text id="knqlsy"
读取目标路径
获取当前位姿
计算轨迹误差
输出速度控制指令
跟踪路径前进
```

验证能力：

```text id="acz3pq"
能连接规划模块和控制模块
能让机器人不只是能动，而是能按路径稳定运动
```

---

### 5.6 高级项目：机械臂关节控制

目标：

```text id="qjs4zj"
控制机械臂多个关节到达目标角度或目标轨迹。
```

功能：

```text id="7btbhi"
读取当前关节角
输入目标关节角
计算关节误差
输出控制指令
执行关节运动
```

验证能力：

```text id="ujn1ix"
能理解多关节机器人控制
能让机械臂执行规划模块生成的动作
能为抓取任务打基础
```

---

### 5.7 高级项目：无人机姿态 / 高度控制仿真

目标：

```text id="hdtmmw"
让无人机在仿真中保持稳定姿态或稳定高度。
```

功能：

```text id="2a958h"
读取无人机当前姿态
读取当前高度
输入目标高度或目标姿态
输出控制指令
保持稳定飞行
```

验证能力：

```text id="el3mab"
能理解无人机控制的基本结构
能将控制理论应用到飞行系统
能为智能无人系统项目打基础
```

---

### 5.8 高级项目：MPC 轨迹跟踪控制

目标：

```text id="lmudbv"
使用模型预测控制让机器人在约束条件下跟踪目标轨迹。
```

功能：

```text id="hgq8na"
建立机器人运动模型
设置目标轨迹
设置速度、加速度或转向约束
优化未来控制量
执行当前控制输入
```

验证能力：

```text id="b08xaa"
能理解约束控制和优化控制
能处理比普通反馈控制更复杂的轨迹跟踪任务
能为无人车、无人机和机械臂高级控制打基础
```

---

## 6. 学习状态记录

| 知识点         | 当前状态 |
| ----------- | ---- |
| 自动控制原理      | 了解   |
| 现代控制理论      | 未开始  |
| 机器人控制       | 未开始  |
| 电机控制        | 入门   |
| 运动控制        | 未开始  |
| 无人机控制       | 了解   |
| 车辆控制        | 未开始  |
| 最优控制与模型预测控制 | 未开始  |
| 学习型控制       | 了解   |

状态标准：

```text id="aj12qm"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

控制模块最终要实现：

```text id="x3y4xr"
智能体能够根据规划模块输出的目标位置、目标速度或目标轨迹生成控制指令；
能够通过反馈控制减少误差；
能够稳定控制电机、底盘、机械臂或无人机；
能够让机器人按照路径或轨迹运动；
能够在约束条件下进行更稳定、更安全的控制；
能够把控制结果交给执行模块完成真实动作。
```

最终效果：

> 智能体不只是知道“怎么规划”，而是能够把规划结果稳定、准确、安全地转化为真实或仿真的身体运动。

