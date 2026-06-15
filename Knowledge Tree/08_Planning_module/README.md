# 08_规划模块

## 1. 模块定位

规划模块负责把任务目标转化为可执行的步骤、路径、轨迹或动作序列。

它回答的问题是：

> 智能体已经知道要做什么之后，具体应该怎么做？

规划模块不负责决定“当前应该做哪个任务”，那是决策模块的职责。
规划模块也不负责直接输出电机 PWM、关节力矩或底层控制量，那是控制模块的职责。

一句话概括：

> 规划模块负责“把目标变成可执行方案”。

在完整具身智能体中，规划模块通常位于决策模块之后、控制模块之前：

```text id="mx6ubx"
决策模块
  ↓
规划模块
  ↓
控制模块
  ↓
执行模块
```

---

## 2. 模块输入

规划模块可能接收以下输入：

```text id="xb53if"
当前任务
目标状态
当前状态
机器人位姿
地图信息
障碍物信息
目标位置
机器人运动约束
环境约束
安全约束
决策模块输出的当前行为
```

例子：

```text id="zsdz9a"
当前任务：把杯子送到厨房
当前状态：机器人在客厅入口
目标状态：杯子位于厨房
地图信息：厨房在地图右侧
障碍物信息：客厅中间有障碍物
机器人约束：底盘不能穿墙，机械臂不能超过关节限制
```

---

## 3. 模块输出

规划模块的输出是可交给控制模块或技能执行模块的计划。

常见输出：

```text id="b37pcr"
任务步骤
路径
轨迹
动作序列
导航路线
运动规划结果
抓取方案
重规划结果
```

例子：

```json id="nd043e"
{
  "plan_type": "task_plan",
  "steps": [
    "navigate_to_table",
    "detect_red_cup",
    "grasp_red_cup",
    "navigate_to_kitchen",
    "place_red_cup"
  ]
}
```

或者：

```json id="ku6xym"
{
  "plan_type": "path_plan",
  "waypoints": [
    [0.0, 0.0],
    [1.2, 0.5],
    [2.4, 1.0],
    [3.0, 2.0]
  ]
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 人工智能规划

作用：

> 将高层任务目标拆解成有顺序、有条件、有依赖关系的任务步骤。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Malik Ghallab, Dana Nau, Paolo Traverso：《Automated Planning: Theory and Practice》
* Patrik Haslum 等：《An Introduction to the Planning Domain Definition Language》

推荐教程 / 网课：

* Berkeley CS188: Introduction to Artificial Intelligence
* AIMA 官方配套资料
* PDDL 教程
* PlanSys2 / ROS 2 Planning System 相关教程

对应项目：

* 简单任务规划器
* PDDL 任务规划实验
* 机器人任务拆解：导航 → 检测 → 抓取 → 放置
* 多阶段配送任务规划
* 失败后的任务重规划

---

### 4.2 路径规划

作用：

> 在地图中为机器人寻找一条从起点到目标点的可行路径。

推荐书籍：

* Steven M. LaValle：《Planning Algorithms》
* Howie Choset 等：《Principles of Robot Motion》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》

推荐教程 / 网课：

* Modern Robotics 路径规划相关章节
* PythonRobotics 路径规划教程
* ROS 2 Navigation2 Planner 文档
* 移动机器人路径规划课程

对应项目：

* 二维网格地图路径规划
* BFS / Dijkstra / A* 路径规划实验
* 小车从 A 点规划到 B 点
* 无人机配送路径规划
* 基于地图的避障路径规划

---

### 4.3 运动规划

作用：

> 在机器人自身运动约束和环境约束下，规划机器人身体或机械臂如何运动。

推荐书籍：

* Steven M. LaValle：《Planning Algorithms》
* Howie Choset 等：《Principles of Robot Motion》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》

推荐教程 / 网课：

* OMPL 官方文档
* MoveIt 2 官方文档
* Modern Robotics Motion Planning 相关章节
* 机器人运动规划公开课

对应项目：

* 机械臂避障运动规划
* 移动机器人配置空间规划
* 使用 OMPL 进行运动规划实验
* 使用 MoveIt 2 规划机械臂动作
* 机器人在约束空间中的可行运动规划

---

### 4.4 轨迹规划

作用：

> 在路径基础上加入时间、速度、加速度等信息，生成机器人可以平滑执行的运动轨迹。

推荐书籍：

* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* Steven M. LaValle：《Planning Algorithms》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》

推荐教程 / 网课：

* Modern Robotics Trajectory Generation 章节
* 移动机器人轨迹规划教程
* 自动驾驶轨迹规划课程
* MoveIt 2 Trajectory Processing 相关教程

对应项目：

* 小车轨迹生成
* 路径平滑实验
* 梯形速度规划
* 机械臂关节轨迹生成
* 无人机平滑航迹生成
* 将路径点转成可执行轨迹

---

### 4.5 机器人导航

作用：

> 综合地图、定位、路径规划、局部避障和控制，让移动机器人自主从一个位置移动到另一个位置。

推荐书籍：

* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》
* Sebastian Thrun, Wolfram Burgard, Dieter Fox：《Probabilistic Robotics》
* Howie Choset 等：《Principles of Robot Motion》

推荐教程 / 网课：

* ROS 2 Navigation2 官方文档
* Navigation2 with SLAM 官方教程
* ROS 2 Nav2 Tutorials
* 自主移动机器人导航课程

对应项目：

* ROS 2 Navigation2 自主导航
* 小车从 A 点导航到 B 点
* 地图导航与动态避障
* 局部路径重规划
* 低电量自动导航到充电桩
* 仿真环境中的自主导航任务

---

### 4.6 机械臂运动规划

作用：

> 让机械臂根据目标位姿和环境约束，生成可执行的关节运动或末端轨迹。

推荐书籍：

* John J. Craig：《Introduction to Robotics: Mechanics and Control》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* Bruno Siciliano 等：《Robotics: Modelling, Planning and Control》

推荐教程 / 网课：

* MoveIt 2 官方文档
* Modern Robotics 机械臂相关章节
* ROS 2 Manipulation 教程
* 机械臂运动规划公开课

对应项目：

* MoveIt 2 控制机械臂
* 机械臂末端到达目标位姿
* 机械臂避障路径规划
* 视觉目标引导机械臂抓取
* 导航到桌子附近后执行抓取规划

---

### 4.7 自动驾驶规划基础

作用：

> 理解更复杂动态环境中的行为规划、路径规划和轨迹规划，对无人车、无人机和移动机器人都有参考价值。

推荐书籍：

* Markus Maurer 等：《Autonomous Driving》
* Raj Rajkumar 等：《Autonomous Vehicle Technology》
* Steven M. LaValle：《Planning Algorithms》

推荐教程 / 网课：

* Coursera Self-Driving Cars Specialization
* Udacity Self-Driving Car Nanodegree 规划部分
* 自动驾驶运动规划公开课
* Apollo / Autoware 规划模块教程

对应项目：

* 简单道路场景路径规划
* 动态障碍物避让
* 行为规划：跟随、避让、停车
* 轨迹候选生成与选择
* 无人车 / 无人机局部规划实验

---

### 4.8 任务与运动结合规划

作用：

> 将高层任务规划、路径规划、运动规划和执行约束结合起来，形成完整机器人任务方案。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Steven M. LaValle：《Planning Algorithms》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》

推荐教程 / 网课：

* Task and Motion Planning 相关课程
* ROS 2 PlanSys2 相关教程
* MoveIt Task Constructor 教程
* 机器人操作任务规划相关教程

对应项目：

* 导航 → 识别 → 抓取 → 放置的完整任务规划
* 移动机械臂任务规划
* 失败后自动重规划
* 多阶段机器人任务执行流程
* 语言任务到机器人动作序列的中间规划层

---

## 5. 项目验证

### 5.1 入门项目：二维网格路径规划

目标：

```text id="42f6pb"
在二维网格地图中，从起点规划到目标点。
```

功能：

```text id="zyrxn7"
读取地图
设置起点
设置目标点
避开障碍物
输出路径
可视化路径
```

验证能力：

```text id="i295zz"
能理解路径规划基本问题
能实现简单搜索规划
能将地图信息转化为路径
```

---

### 5.2 入门项目：任务步骤规划器

目标：

```text id="27j7tm"
把一个高层任务拆成多个执行步骤。
```

示例任务：

```text id="ndgqjf"
把红色杯子放到厨房
```

输出步骤：

```text id="ab923k"
导航到桌子
检测红色杯子
抓取红色杯子
导航到厨房
放下红色杯子
检查任务结果
```

验证能力：

```text id="p1v9em"
能把任务目标转化为步骤序列
能理解任务规划和路径规划的区别
能为决策和执行模块提供中间层
```

---

### 5.3 进阶项目：ROS 2 Navigation2 自主导航

目标：

```text id="er8u3g"
让移动机器人基于地图自主导航到目标点。
```

功能：

```text id="v25i1l"
加载地图
定位机器人
设置目标点
全局路径规划
局部避障
到达目标
```

验证能力：

```text id="qoh125"
能使用 ROS 2 导航框架
能理解全局规划和局部规划
能让路径规划真正接入机器人系统
```

---

### 5.4 进阶项目：动态障碍物重规划

目标：

```text id="hxbh4n"
在环境变化时，让机器人重新规划路线。
```

示例流程：

```text id="c2ah8e"
原路径可行
↓
前方出现障碍物
↓
局部地图更新
↓
规划模块重新规划
↓
机器人绕开障碍物
```

验证能力：

```text id="1q74l6"
能处理动态环境
能理解规划和状态模块的配合
能让机器人不只是沿固定路径执行
```

---

### 5.5 进阶项目：MoveIt 2 机械臂运动规划

目标：

```text id="xj0r0d"
使用 MoveIt 2 为机械臂生成可执行运动。
```

功能：

```text id="ipsvba"
加载机械臂模型
设置目标位姿
碰撞检测
生成关节轨迹
执行规划结果
```

验证能力：

```text id="hr91kf"
能理解机械臂运动规划
能使用机器人规划工具
能将目标位姿转化为机械臂动作
```

---

### 5.6 高级项目：导航 + 抓取 + 放置任务规划

目标：

```text id="a9z29q"
将移动导航、视觉检测、机械臂规划和任务步骤组织成完整流程。
```

示例流程：

```text id="a7g9ty"
导航到桌子附近
↓
视觉检测目标
↓
机械臂抓取规划
↓
导航到放置区域
↓
机械臂放置规划
↓
检查任务完成
```

验证能力：

```text id="ioprb1"
能将任务规划、路径规划和运动规划结合
能形成接近真实机器人系统的完整规划链路
```

---

### 5.7 高级项目：无人机配送路径规划

目标：

```text id="glvfpz"
为无人机配送任务设计路径规划和重规划机制。
```

功能：

```text id="g4i0zd"
从当前位置规划到仓库
从仓库规划到驿站
低电量规划到充电桩
遇到障碍物重新规划
根据任务优先级选择目标
```

验证能力：

```text id="g7zktw"
能将路径规划应用到无人机配送任务
能处理充电、投递、避障等复杂条件
能和已有无人机 RL 项目形成连接
```

---

### 5.8 高级项目：任务与运动结合规划原型

目标：

```text id="cdyxqs"
实现一个从高层任务到低层运动方案的完整规划原型。
```

输入：

```text id="6h85m9"
任务目标
当前状态
地图
机器人约束
环境约束
```

输出：

```text id="0j2e8n"
任务步骤
导航路径
机械臂运动轨迹
失败重规划方案
```

验证能力：

```text id="h04da8"
能理解具身智能中的规划不是单一算法
能将多层规划连接成完整系统
能为后续语言驱动机器人和 VLA 系统打基础
```

---

## 6. 学习状态记录

| 知识点       | 当前状态 |
| --------- | ---- |
| 人工智能规划    | 了解   |
| 路径规划      | 入门   |
| 运动规划      | 未开始  |
| 轨迹规划      | 未开始  |
| 机器人导航     | 未开始  |
| 机械臂运动规划   | 未开始  |
| 自动驾驶规划基础  | 未开始  |
| 任务与运动结合规划 | 未开始  |

状态标准：

```text id="t0mnwm"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

规划模块最终要实现：

```text id="src9q3"
智能体能够把目标任务拆解成可执行步骤；
能够根据地图和障碍物生成路径；
能够根据机器人运动约束生成轨迹；
能够为机械臂、移动机器人或无人机生成运动方案；
能够在环境变化、路径失败或任务失败时重新规划；
能够把规划结果传给控制模块或技能执行模块。
```

最终效果：

> 智能体不只是知道“要做什么”，而是能够把目标转化为具体步骤、可行路径、可执行轨迹和失败后的重规划方案。

