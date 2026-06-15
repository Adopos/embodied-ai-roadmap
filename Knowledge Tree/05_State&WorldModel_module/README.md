# 05_状态与世界模型模块

## 1. 模块定位

状态与世界模型模块负责维护智能体自身状态、环境状态、地图信息和任务相关世界表示。

它回答的问题是：

> 智能体现在在哪里？周围环境是什么样？目标在哪里？障碍物在哪里？当前世界处于什么状态？

状态与世界模型模块不是直接“看见世界”的模块。
“看见世界”是感知模块的任务；
“把感知结果整合成可用于决策、规划和控制的世界状态”，才是状态与世界模型模块的任务。

一句话概括：

> 状态与世界模型模块负责“把零散感知信息整合成智能体可使用的当前世界状态”。

在完整具身智能体中，它通常位于感知模块之后、决策和规划模块之前：

```text id="e3geee"
感知模块
  ↓
状态 / 世界模型模块
  ↓
决策模块
  ↓
规划模块
  ↓
控制与执行模块
```

---

## 2. 模块输入

状态与世界模型模块可能接收以下输入：

```text id="58hxfz"
摄像头感知结果
深度相机数据
LiDAR 点云
IMU 数据
编码器数据
GPS 数据
机器人关节状态
电量状态
任务状态
历史轨迹
地图数据
感知模块输出的目标、障碍物和语义信息
```

例子：

```text id="r2stmp"
机器人当前位置估计
机器人速度
机器人姿态
目标物体检测结果
障碍物检测结果
局部地图
全局地图
电量信息
机械臂关节状态
```

---

## 3. 模块输出

状态与世界模型模块的输出是智能体当前可用的世界状态。

常见输出：

```text id="ctoad5"
机器人位姿
机器人速度
机器人姿态
机器人自身状态
目标物体位置
障碍物位置
局部地图
全局地图
占据栅格地图
语义地图
任务相关状态
环境动态变化
可导航区域
风险区域
世界状态表示
```

例子：

```json id="a46gsv"
{
  "robot_pose": {
    "x": 2.4,
    "y": 1.7,
    "theta": 0.8
  },
  "battery": 0.65,
  "target_object": {
    "name": "red_cup",
    "position": [3.2, 2.1]
  },
  "nearest_obstacle_distance": 1.3
}
```

或者：

```json id="1yazjz"
{
  "map_type": "occupancy_grid",
  "robot_location": "living_room",
  "target_location": "kitchen",
  "task_state": "navigating_to_target"
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 机器人学

作用：

> 为理解机器人位姿、坐标系、运动学、地图、导航和控制提供基础。

推荐书籍：

* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* John J. Craig：《Introduction to Robotics: Mechanics and Control》
* Richard M. Murray, Zexiang Li, S. Shankar Sastry：《A Mathematical Introduction to Robotic Manipulation》

推荐教程 / 网课：

* Modern Robotics Coursera Specialization
* Northwestern Modern Robotics 官方课程资源
* 中国大学 MOOC / B站机器人学课程
* ROS 2 机器人学基础教程

对应项目：

* 机器人位姿表示实验
* 坐标系转换实验
* 移动机器人运动学建模
* 机械臂正逆运动学实验
* 建立机器人自身状态表示

---

### 4.2 坐标变换与空间几何

作用：

> 让智能体能够统一表示机器人、传感器、目标物体和地图之间的空间关系。

推荐书籍：

* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* Richard M. Murray, Zexiang Li, S. Shankar Sastry：《A Mathematical Introduction to Robotic Manipulation》
* Hartley, Zisserman：《Multiple View Geometry in Computer Vision》

推荐教程 / 网课：

* Modern Robotics 坐标变换相关章节
* ROS 2 TF2 官方教程
* OpenCV 相机标定与三维重建教程
* 视觉 SLAM 坐标变换相关教程

对应项目：

* ROS 2 TF 坐标变换实验
* 相机坐标系到机器人坐标系转换
* LiDAR 坐标系到底盘坐标系转换
* 地图坐标系、里程计坐标系和机器人坐标系管理
* 目标物体三维位置转换到机器人可执行坐标

---

### 4.3 状态估计

作用：

> 从带噪声的传感器数据中估计机器人当前状态，例如位置、速度、姿态和不确定性。

推荐书籍：

* Timothy D. Barfoot：《State Estimation for Robotics》
* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Yaakov Bar-Shalom 等：《Estimation with Applications to Tracking and Navigation》

推荐教程 / 网课：

* State Estimation for Robotics 相关课程
* Probabilistic Robotics 相关课程
* Kalman Filter / Bayesian Filtering 系统教程
* robot_localization 官方文档

对应项目：

* 编码器里程计状态估计
* IMU 姿态估计
* 小车位置与速度估计
* GPS / IMU / 编码器状态融合
* 使用 robot_localization 进行机器人状态估计

---

### 4.4 传感器融合

作用：

> 将多个传感器的信息融合成更稳定、更准确的机器人状态。

推荐书籍：

* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Timothy D. Barfoot：《State Estimation for Robotics》
* David L. Hall, James Llinas：《Handbook of Multisensor Data Fusion》

推荐教程 / 网课：

* robot_localization 官方文档
* ROS 2 Sensor Fusion 教程
* Kalman Filter / Extended Kalman Filter 教程
* Autonomous Robots / Self-Driving Cars 传感器融合课程

对应项目：

* 编码器 + IMU 融合
* GPS + IMU 融合
* LiDAR + IMU 融合
* 视觉 + IMU 融合
* 使用 robot_localization 输出稳定里程计

---

### 4.5 SLAM

作用：

> 让机器人在未知环境中同时完成定位和建图。

推荐书籍：

* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Timothy D. Barfoot：《State Estimation for Robotics》
* Cyrill Stachniss 相关 SLAM 讲义
* 高翔：《视觉 SLAM 十四讲》

推荐教程 / 网课：

* Cyrill Stachniss SLAM Course
* ROS 2 SLAM Toolbox 官方文档
* Navigation2 with SLAM 官方教程
* Cartographer 官方文档
* SLAM 入门系统教程

对应项目：

* 运行 SLAM Toolbox 建图
* 使用 ROS 2 保存二维地图
* 在仿真环境中完成 SLAM
* 在真实小车上完成室内建图
* 将 SLAM 地图接入导航系统

---

### 4.6 视觉 SLAM

作用：

> 使用相机进行定位和建图，适合无人机、移动机器人、AR 和视觉导航场景。

推荐书籍：

* 高翔：《视觉 SLAM 十四讲》
* Richard Hartley, Andrew Zisserman：《Multiple View Geometry in Computer Vision》
* Timothy D. Barfoot：《State Estimation for Robotics》

推荐教程 / 网课：

* 视觉 SLAM 十四讲配套教程
* ORB-SLAM / ORB-SLAM3 开源教程
* VINS-Mono / VINS-Fusion 教程
* 多视图几何与视觉里程计课程

对应项目：

* 单目视觉里程计实验
* 双目视觉里程计实验
* RGB-D 视觉 SLAM 实验
* 运行 ORB-SLAM / ORB-SLAM3
* 运行 VINS-Mono / VINS-Fusion
* 使用相机完成机器人定位与建图

---

### 4.7 激光 SLAM

作用：

> 使用 LiDAR 进行定位和建图，适合移动机器人、无人车、室内导航和室外导航场景。

推荐书籍：

* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Timothy D. Barfoot：《State Estimation for Robotics》
* 《Introduction to Autonomous Robots》

推荐教程 / 网课：

* SLAM Toolbox 官方文档
* Cartographer 官方文档
* LOAM / LeGO-LOAM / LIO-SAM 开源教程
* FAST-LIO / FAST-LIO2 开源教程
* ROS 2 LiDAR SLAM 教程

对应项目：

* 使用 2D LiDAR 运行 SLAM Toolbox
* 使用 Cartographer 建图
* 运行 LeGO-LOAM / LIO-SAM
* LiDAR + IMU 建图
* 使用激光地图进行自主导航

---

### 4.8 地图构建

作用：

> 将环境表示成机器人可用于定位、规划、避障和任务执行的地图。

推荐书籍：

* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* 《Introduction to Autonomous Robots》
* Howie Choset 等：《Principles of Robot Motion》

推荐教程 / 网课：

* ROS 2 Navigation2 地图相关教程
* SLAM Toolbox 地图保存与定位教程
* Cartographer 地图构建教程
* Occupancy Grid Mapping 教程

对应项目：

* 构建二维占据栅格地图
* 保存和加载地图
* 构建局部地图与全局地图
* 标记障碍物区域
* 标记可导航区域
* 将地图用于路径规划和避障

---

### 4.9 机器人定位与导航基础

作用：

> 让机器人知道自己在地图中的位置，并能基于地图进行移动。

推荐书籍：

* 《Introduction to Autonomous Robots》
* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Howie Choset 等：《Principles of Robot Motion》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics》

推荐教程 / 网课：

* ROS 2 Navigation2 官方文档
* Navigation2 with SLAM 官方教程
* ROS 2 Localization 教程
* Autonomous Mobile Robots 相关课程

对应项目：

* 使用 AMCL 进行定位
* 地图中机器人重定位
* 从 A 点导航到 B 点
* 动态障碍环境下更新局部状态
* 使用 Navigation2 完成自主导航

---

### 4.10 世界模型

作用：

> 建立智能体对当前世界和未来世界变化的内部表示，为决策、规划和学习提供支持。

这里的世界模型包括两层含义：

```text id="9m8rxs"
工程层面：
维护当前环境状态、机器人状态、任务状态和地图状态。

学习层面：
学习环境动态，预测未来状态，用于模型预测、强化学习和规划。
```

推荐书籍：

* David Silver 强化学习课程相关资料
* Sutton, Barto：《Reinforcement Learning: An Introduction》
* Kevin Murphy：《Probabilistic Machine Learning》
* Ian Goodfellow, Yoshua Bengio, Aaron Courville：《Deep Learning》

推荐教程 / 网课：

* Dreamer / World Models 相关教程
* Model-based Reinforcement Learning 课程
* Hugging Face Deep RL Course
* DeepMind / Google Research 世界模型相关博客和论文教程

对应项目：

* 简单网格世界状态表示
* 无人机配送环境状态表示
* 机器人任务世界状态字典
* 基于历史状态预测下一步状态
* Dreamer / Model-based RL 小实验
* 将世界状态传给决策和规划模块

---

## 5. 项目验证

### 5.1 入门项目：机器人状态表示系统

目标：

```text id="4x9r4q"
建立一个简单机器人状态字典，统一保存机器人自身状态和任务相关状态。
```

示例状态：

```json id="v5b4jv"
{
  "robot_position": [2.0, 1.5],
  "robot_heading": 0.7,
  "battery": 0.65,
  "task_state": "moving_to_target",
  "nearest_obstacle": 1.2
}
```

验证能力：

```text id="4b4u44"
能定义机器人当前状态
能让决策模块读取状态
能根据感知结果更新状态
```

---

### 5.2 入门项目：编码器 + IMU 状态估计

目标：

```text id="8y34a1"
使用编码器和 IMU 估计小车的运动状态。
```

功能：

```text id="m6noix"
读取编码器
读取 IMU
估计速度
估计方向
估计相对位移
```

验证能力：

```text id="9g4v7m"
能理解机器人自身状态
能处理简单传感器数据
能输出可用于控制和规划的状态信息
```

---

### 5.3 进阶项目：ROS 2 TF 坐标变换实验

目标：

```text id="s9i8hw"
在 ROS 2 中维护机器人各坐标系之间的关系。
```

涉及坐标系：

```text id="781avz"
map
odom
base_link
camera_link
laser_link
```

验证能力：

```text id="q5949p"
能理解机器人坐标系统
能管理传感器与机器人本体之间的关系
能为导航和感知提供统一空间表示
```

---

### 5.4 进阶项目：robot_localization 传感器融合

目标：

```text id="kt4v77"
使用 robot_localization 融合 IMU、编码器、GPS 或其他里程计信息。
```

功能：

```text id="ygvmd1"
配置传感器输入
输出融合后的 odometry
发布稳定机器人位姿
接入导航系统
```

验证能力：

```text id="wcjjh1"
能使用现成状态估计工具
能理解多传感器融合流程
能为导航模块提供可靠状态
```

---

### 5.5 进阶项目：SLAM Toolbox 建图

目标：

```text id="58bak7"
使用 2D LiDAR 和 SLAM Toolbox 构建室内地图。
```

功能：

```text id="74d9xg"
读取 LiDAR 数据
运行 SLAM
生成地图
保存地图
加载地图
```

验证能力：

```text id="1jfc00"
能完成机器人建图
能理解地图与定位之间的关系
能为导航模块提供地图
```

---

### 5.6 高级项目：视觉 SLAM / 激光 SLAM 实验

目标：

```text id="b0pczx"
使用相机或 LiDAR 完成更复杂的定位与建图。
```

可选方向：

```text id="to1snf"
ORB-SLAM / ORB-SLAM3
VINS-Mono / VINS-Fusion
Cartographer
LIO-SAM
FAST-LIO
```

验证能力：

```text id="eu2lga"
能运行典型 SLAM 系统
能理解视觉 / 激光定位建图的基本流程
能输出轨迹和地图
```

---

### 5.7 高级项目：世界状态接入决策与规划

目标：

```text id="fe3hc4"
让世界状态真正参与智能体决策和规划。
```

示例流程：

```text id="zc5d5e"
感知模块检测到障碍物
↓
状态模块更新局部地图
↓
决策模块判断是否避障
↓
规划模块重新规划路径
```

验证能力：

```text id="m5xnop"
状态信息不只是被记录，而是能影响智能体后续行为。
```

---

### 5.8 高级项目：简单世界模型实验

目标：

```text id="mri03a"
让智能体根据当前状态和动作预测下一步状态。
```

示例：

```text id="xgt2gj"
输入：
当前状态 + 动作

输出：
下一步状态预测
```

验证能力：

```text id="q1wigj"
能理解世界模型的基本思想
能将状态表示、预测和决策联系起来
能为后续 Model-based RL / Dreamer / VLA 打基础
```

---

## 6. 学习状态记录

| 知识点        | 当前状态 |
| ---------- | ---- |
| 机器人学       | 未开始  |
| 坐标变换与空间几何  | 未开始  |
| 状态估计       | 未开始  |
| 传感器融合      | 未开始  |
| SLAM       | 未开始  |
| 视觉 SLAM    | 未开始  |
| 激光 SLAM    | 未开始  |
| 地图构建       | 未开始  |
| 机器人定位与导航基础 | 未开始  |
| 世界模型       | 了解   |

状态标准：

```text id="3f7xul"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

状态与世界模型模块最终要实现：

```text id="z915n3"
智能体能够维护自身状态；
能够统一管理机器人、传感器、目标和地图之间的空间关系；
能够融合多种传感器信息；
能够完成定位、建图和地图更新；
能够表示当前任务相关的世界状态；
能够把状态信息传给决策模块、规划模块和控制模块；
能够为后续世界模型、机器人学习和 VLA 系统打基础。
```

最终效果：

> 智能体不只是“看见”环境，而是能够持续维护一个可用于行动的内部世界表示。

