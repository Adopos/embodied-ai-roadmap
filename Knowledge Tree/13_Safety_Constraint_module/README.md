
# 13_安全约束模块

## 1. 模块定位

安全约束模块负责保证具身智能体在执行任务时不发生危险行为，并在异常情况出现时及时限制、停止、恢复或请求人工接管。

它回答的问题是：

> 智能体哪些事情绝对不能做？什么时候必须停止？什么时候必须降级运行？如何避免伤人、撞坏设备、损坏环境或任务失控？

安全约束模块不是单独位于某一个流程节点的模块，而是横向监督整个具身智能体系统。

它会影响：

```text id="bq2zf8"
任务管理
决策
规划
控制
执行
反馈评价
学习
```

一句话概括：

> 安全约束模块负责“给智能体的所有行为加上安全边界”。

在完整具身智能体中，它更像一个横向保护层：

```text id="u25aeg"
交互 → 任务 → 感知 → 状态 → 决策 → 规划 → 控制 → 执行 → 反馈 → 学习
   ↑       ↑       ↑       ↑       ↑       ↑       ↑       ↑
   └────────────── 安全 / 约束模块横向监督 ──────────────┘
```

---

## 2. 模块输入

安全约束模块可能接收以下输入：

```text id="tjil5z"
机器人当前位置
机器人速度
机器人姿态
机器人电量
障碍物距离
人体检测结果
机械臂关节状态
电机电流
电机温度
通信状态
传感器状态
任务状态
规划路径
控制指令
执行反馈
学习策略输出
系统异常信息
```

例子：

```text id="cc2x2x"
前方 0.3 m 有障碍物
电量低于 15%
机械臂关节接近限位
电机电流过大
通信中断
LiDAR 数据停止更新
规划路径穿过障碍物
RL 策略输出危险动作
```

---

## 3. 模块输出

安全约束模块的输出是限制、修正、拒绝或中断信号。

常见输出：

```text id="vnmax1"
急停信号
限速信号
限位信号
低电量保护信号
重新规划信号
拒绝执行信号
任务中断信号
请求人工接管信号
安全模式信号
故障报警
异常日志
风险等级
```

例子：

```json id="snw45p"
{
  "safety_action": "emergency_stop",
  "reason": "obstacle_too_close",
  "distance": 0.3
}
```

或者：

```json id="5n7bd5"
{
  "safety_action": "limit_velocity",
  "reason": "human_detected_nearby",
  "max_speed": 0.2
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 机器人安全

作用：

> 理解机器人系统中的危险源、风险评估、安全边界、防护措施和安全设计原则。

推荐书籍：

* Bruno Siciliano 等：《Springer Handbook of Robotics》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》
* 《Robot Safety: Current and Emerging Trends》

推荐教程 / 网课：

* ISO 10218 机器人安全标准资料
* ISO/TS 15066 协作机器人安全资料
* OSHA / NIOSH 机器人安全资料
* 协作机器人安全培训课程
* 工业机器人安全课程

对应项目：

* 机器人危险源清单
* 小车障碍物急停
* 机械臂安全工作空间限制
* 人靠近时机器人减速或停止
* 机器人任务前安全检查流程

---

### 4.2 故障检测与诊断

作用：

> 发现传感器失效、执行器异常、通信中断、电机过载、定位异常等问题，并判断故障类型和严重程度。

推荐书籍：

* Rolf Isermann：《Fault-Diagnosis Systems》
* Steven X. Ding：《Model-Based Fault Diagnosis Techniques》
* Janos Gertler：《Fault Detection and Diagnosis in Engineering Systems》

推荐教程 / 网课：

* Fault Detection and Diagnosis 相关课程
* Control Systems Fault Diagnosis 教程
* ROS Diagnostics / diagnostic_updater 教程
* ROS 2 Logging 和系统监控教程
* 机器人系统健康监控教程

对应项目：

* 传感器掉线检测
* LiDAR 数据超时检测
* IMU 数据异常检测
* 电机堵转检测
* 通信中断检测
* 机器人故障状态面板

---

### 4.3 可靠性工程

作用：

> 从系统工程角度提升机器人长期运行稳定性，减少随机故障、设计缺陷和运行中断。

推荐书籍：

* Patrick D. T. O’Connor, Andre Kleyner：《Practical Reliability Engineering》
* Elsayed A. Elsayed：《Reliability Engineering》
* Betsy Beyer 等：《Site Reliability Engineering》

推荐教程 / 网课：

* Google SRE Book / SRE Workbook
* Reliability Engineering 公开课
* 系统可靠性分析课程
* FMEA / FTA 教程
* 工程可靠性与维护课程

对应项目：

* 机器人故障模式分析
* 任务失败原因分类
* 长时间运行稳定性测试
* 系统异常日志分析
* 机器人自检流程
* 关键模块冗余设计思路

---

### 4.4 安全控制

作用：

> 在控制层面对速度、位置、力矩、电流、姿态和关节范围进行约束，防止危险控制指令被执行。

推荐书籍：

* Katsuhiko Ogata：《Modern Control Engineering》
* Gene F. Franklin 等：《Feedback Control of Dynamic Systems》
* Rajesh Rajamani：《Vehicle Dynamics and Control》

推荐教程 / 网课：

* MIT Feedback Systems
* Control Barrier Functions 相关教程
* Safety-Critical Control 相关课程
* ROS 2 Control 官方文档
* PX4 安全与 failsafe 相关文档

对应项目：

* 小车限速控制
* 机械臂关节限位保护
* 电机电流限制
* 无人机高度限制
* 距离障碍物过近时自动减速
* 控制指令安全过滤器

---

### 4.5 约束优化

作用：

> 在速度、加速度、障碍物、电量、关节范围等约束下求解安全可行的路径、轨迹或控制输入。

推荐书籍：

* Stephen Boyd, Lieven Vandenberghe：《Convex Optimization》
* Dimitri P. Bertsekas：《Nonlinear Programming》
* Jorge Nocedal, Stephen Wright：《Numerical Optimization》

推荐教程 / 网课：

* Stanford Convex Optimization 课程
* Boyd Convex Optimization 公开资料
* CasADi 官方教程
* CVXPY 官方教程
* Model Predictive Control 相关课程

对应项目：

* 限速条件下的路径规划
* 避障约束下的轨迹优化
* 低电量约束下的任务选择
* 机械臂关节限制下的运动规划
* MPC 安全轨迹跟踪实验

---

### 4.6 风险评估

作用：

> 识别任务、环境、动作和系统状态中的风险，并为决策、规划和控制提供风险等级。

推荐书籍：

* Marvin Rausand：《Risk Assessment: Theory, Methods, and Applications》
* Terje Aven：《Risk Analysis》
* Nancy Leveson：《Engineering a Safer World》

推荐教程 / 网课：

* Risk Assessment 公开课
* System Safety Engineering 课程
* FMEA / HAZOP 教程
* Autonomous Systems Risk Assessment 教程
* 机器人任务风险评估教程

对应项目：

* 任务风险评分系统
* 区域风险地图
* 动态障碍物风险评估
* 低电量任务风险评估
* 抓取任务失败风险评估
* 决策前安全风险检查

---

### 4.7 安全强化学习

作用：

> 在强化学习过程中加入安全约束，避免智能体在探索或执行时产生危险动作。

推荐书籍：

* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Dimitri P. Bertsekas：《Reinforcement Learning and Optimal Control》
* Mykel J. Kochenderfer：《Decision Making Under Uncertainty》

推荐教程 / 网课：

* CMU Safe Autonomy / Safe RL 相关课程
* Berkeley CS285 相关内容
* Safe Reinforcement Learning 综述论文与教程
* Constrained Reinforcement Learning 教程
* Shielded RL / Safe Exploration 相关教程

对应项目：

* 带碰撞惩罚的 RL 小车导航
* 加入安全约束的无人机配送 RL
* RL 动作安全过滤器
* 低电量约束下的 RL 任务决策
* 对比普通 RL 和安全 RL 的任务表现
* 安全探索小实验

---

### 4.8 嵌入式安全机制

作用：

> 在下位机和硬件层面处理过流、过温、欠压、通信中断、急停和执行器异常。

推荐书籍：

* David E. Simon：《An Embedded Software Primer》
* Jonathan W. Valvano：《Embedded Systems: Introduction to ARM Cortex-M Microcontrollers》
* Miro Samek：《Practical UML Statecharts in C/C++》

推荐教程 / 网课：

* STM32 Functional Safety 官方资料
* ST Motor Control 安全保护资料
* 嵌入式看门狗教程
* STM32 Watchdog / Brown-out Reset / Fault Handler 教程
* 电机驱动保护教程

对应项目：

* 看门狗复位
* 通信超时停车
* 电机过流保护
* 电池欠压保护
* 急停按钮
* 下位机安全状态机
* 执行器故障保护逻辑

---

### 4.9 人机协作安全

作用：

> 保证机器人与人类共处或协作时，能够避免撞击、夹伤、误触发和危险接近。

推荐书籍：

* Bruno Siciliano 等：《Springer Handbook of Robotics》
* Michael A. Goodrich, Alan C. Schultz：《Human-Robot Interaction: A Survey》
* Alan Dix 等：《Human-Computer Interaction》

推荐教程 / 网课：

* Human-Robot Interaction 公开课
* ISO/TS 15066 协作机器人安全资料
* HRI 机器人安全教程
* 协作机器人安全培训
* 人体检测与安全区域监控教程

对应项目：

* 人靠近时机器人减速
* 人进入危险区域时急停
* 机械臂安全工作区限制
* 摄像头 / LiDAR 人体检测
* 人机协作任务安全检查
* 机器人状态提示灯或语音提醒

---

### 4.10 形式化验证与安全验证

作用：

> 用数学方法验证某些系统行为是否满足安全约束，适合自动驾驶、无人机、机器人和安全关键系统。

推荐书籍：

* Christel Baier, Joost-Pieter Katoen：《Principles of Model Checking》
* Edmund M. Clarke 等：《Model Checking》
* Nancy Leveson：《Engineering a Safer World》

推荐教程 / 网课：

* Formal Verification 公开课
* Model Checking 教程
* Reachability Analysis 教程
* CMU Safe Autonomy 相关课程
* Autonomous Systems Verification 相关课程

对应项目：

* 状态机安全性质检查
* 机器人任务流程安全检查
* 规划路径安全验证
* 控制策略输出范围验证
* 安全规则单元测试
* 简单可达性分析实验

---

## 5. 项目验证

### 5.1 入门项目：小车障碍物急停

目标：

```text id="j33cea"
当小车前方障碍物距离过近时，立即停止运动。
```

功能：

```text id="bidkr8"
读取距离传感器
判断安全距离
触发停止指令
记录急停原因
恢复后继续任务
```

验证能力：

```text id="cq0ddr"
能实现最基本的安全保护
能阻止明显危险动作
能让安全模块影响执行模块
```

---

### 5.2 入门项目：低电量保护

目标：

```text id="gaux9a"
当机器人电量过低时，中断普通任务并触发回充或停止。
```

功能：

```text id="03ukx3"
读取电池电量
判断电量阈值
限制高功耗动作
触发回充任务
电量过低时停止执行
```

验证能力：

```text id="6a3m8k"
能根据系统状态触发安全约束
能防止机器人因电量不足导致任务失败或失控
```

---

### 5.3 入门项目：通信断开自动停车

目标：

```text id="wj85dj"
当上位机与下位机通信中断时，机器人自动停止。
```

功能：

```text id="4qu5qq"
检测通信心跳
判断通信超时
停止电机输出
进入安全模式
恢复通信后等待确认
```

验证能力：

```text id="zyw9mx"
能处理通信异常
能避免失联后机器人继续运动
能形成真实机器人安全底线
```

---

### 5.4 进阶项目：机械臂关节限位保护

目标：

```text id="xr4nx1"
防止机械臂关节超过安全角度范围。
```

功能：

```text id="p0i777"
读取当前关节角
检查目标关节角
限制非法目标
拒绝危险动作
记录限位事件
```

验证能力：

```text id="yld33d"
能保护机械结构
能过滤控制模块输出的危险指令
能为机械臂抓取任务提供安全边界
```

---

### 5.5 进阶项目：机器人故障检测系统

目标：

```text id="4tebki"
检测传感器、执行器、通信和任务状态中的异常。
```

检测对象：

```text id="faodg8"
LiDAR 是否掉线
IMU 是否异常
编码器数据是否突变
电机是否堵转
通信是否超时
任务是否超时
定位是否丢失
```

验证能力：

```text id="bpqj90"
能监控机器人运行状态
能识别常见故障
能将故障信息传给任务管理和反馈评价模块
```

---

### 5.6 进阶项目：安全规则管理器

目标：

```text id="kbde1d"
集中管理机器人运行中的安全规则。
```

规则示例：

```text id="e57zfe"
距离障碍物小于阈值：急停
电量低于阈值：回充
速度超过上限：限速
通信超时：停车
机械臂超限：拒绝执行
人靠近：减速
```

验证能力：

```text id="i0fibj"
能统一管理安全约束
能让安全模块横向影响决策、规划、控制和执行
```

---

### 5.7 高级项目：RL 动作安全过滤器

目标：

```text id="e2ie6x"
对强化学习策略输出的动作进行安全检查，防止危险动作直接执行。
```

流程：

```text id="19anxk"
RL 策略输出动作
↓
安全过滤器检查动作
↓
安全：允许执行
危险：修正或拒绝
↓
控制 / 执行模块执行安全动作
```

验证能力：

```text id="gj2n1d"
能将学习型决策与硬安全约束结合
能避免 RL 策略探索过程中的危险行为
能为安全强化学习打基础
```

---

### 5.8 高级项目：机器人安全管理器

目标：

```text id="c4ozg9"
构建一个统一的机器人安全管理系统。
```

功能：

```text id="jc4qy7"
急停
限速
低电量保护
通信异常保护
传感器异常检测
执行器异常检测
任务超时检测
风险等级评估
安全日志记录
人工接管接口
```

验证能力：

```text id="57eava"
能形成完整安全约束模块
能支撑真实机器人长期运行
能让具身智能体具备基本安全底线
```

---

### 5.9 高级项目：人机协作安全原型

目标：

```text id="26hmxy"
在人类靠近机器人时，自动调整机器人行为。
```

功能：

```text id="ojsy1v"
检测人体位置
判断安全距离
进入减速模式
必要时急停
提示用户机器人状态
记录安全事件
```

验证能力：

```text id="pkoezy"
能理解机器人在人类环境中运行的安全要求
能将感知、安全和执行模块结合起来
```

---

## 6. 学习状态记录

| 知识点        | 当前状态 |
| ---------- | ---- |
| 机器人安全      | 未开始  |
| 故障检测与诊断    | 未开始  |
| 可靠性工程      | 未开始  |
| 安全控制       | 未开始  |
| 约束优化       | 未开始  |
| 风险评估       | 未开始  |
| 安全强化学习     | 了解   |
| 嵌入式安全机制    | 未开始  |
| 人机协作安全     | 未开始  |
| 形式化验证与安全验证 | 未开始  |

状态标准：

```text id="bun0m0"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

安全约束模块最终要实现：

```text id="xc3m9f"
智能体能够识别危险状态；
能够在障碍物过近、低电量、通信中断、传感器异常、执行器异常等情况下触发保护；
能够限制危险速度、危险路径、危险动作和危险控制指令；
能够拒绝不安全任务；
能够在必要时急停、降级运行或请求人工接管；
能够为强化学习、规划、控制和执行模块提供安全边界；
能够记录安全事件并用于后续复盘和改进。
```

最终效果：

> 智能体不只是“能完成任务”，而是能够在真实或仿真环境中更安全、更可靠、更可控地完成任务。
