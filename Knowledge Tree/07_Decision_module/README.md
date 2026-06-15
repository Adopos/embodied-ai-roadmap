# 07_决策模块

## 1. 模块定位

决策模块负责根据当前任务、当前状态、历史记忆和安全约束，判断智能体下一步应该做什么。

它回答的问题是：

> 智能体现在应该执行哪个任务？选择哪个技能？采取哪种策略？是否需要切换任务、重新规划或请求人工帮助？

决策模块不负责生成详细路径，也不直接控制电机。

它主要负责选择行为方向，例如：

```text id="zszdl0"
继续执行当前任务
切换到回充任务
开始避障
重新规划路径
选择抓取技能
请求人工帮助
进入安全模式
```

一句话概括：

> 决策模块负责“在当前情况下选择下一步要做什么”。

在完整具身智能体中，决策模块通常位于任务管理、状态与世界模型、记忆模块之后，规划模块之前：

```text id="tqknid"
任务管理模块
状态 / 世界模型模块
记忆模块
安全 / 约束模块
        ↓
决策模块
        ↓
规划模块
```

---

## 2. 模块输入

决策模块可能接收以下输入：

```text id="qbylpo"
当前任务
任务优先级
任务状态
机器人当前位置
机器人电量
障碍物信息
目标位置
地图信息
历史任务经验
失败案例
安全约束
人类反馈
学习模块输出的策略
```

例子：

```text id="iusd6w"
当前任务：配送包裹
当前位置：仓库附近
目标位置：驿站
电量：18%
障碍物：前方有动态障碍
历史经验：低电量继续配送容易失败
安全约束：电量低于 20% 优先回充
```

---

## 3. 模块输出

决策模块的输出是高层行为选择或策略选择。

常见输出：

```text id="5wko19"
当前子任务
当前行为
当前策略
技能选择
任务切换信号
重新规划信号
安全模式信号
是否请求人工帮助
是否继续当前任务
```

例子：

```json id="06g64y"
{
  "decision": "return_to_charger",
  "reason": "low_battery",
  "priority": "high"
}
```

或者：

```json id="fma7qk"
{
  "decision": "replan_path",
  "reason": "dynamic_obstacle_detected",
  "target": "station_3"
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 人工智能导论

作用：

> 建立智能体、搜索、推理、规划、决策和学习的整体框架，是理解决策模块的基础。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Elaine Rich, Kevin Knight, Shivashankar Nair：《Artificial Intelligence》
* Nils J. Nilsson：《Artificial Intelligence: A New Synthesis》

推荐教程 / 网课：

* Berkeley CS188: Introduction to Artificial Intelligence
* MIT Artificial Intelligence 相关课程
* Stanford AI 相关课程
* AIMA 官方配套资料

对应项目：

* 简单理性智能体
* 网格世界决策智能体
* 搜索与决策小实验
* 简单任务选择系统
* 基于规则的机器人行为选择器

---

### 4.2 决策理论与不确定性推理

作用：

> 让智能体在信息不完整、环境不确定、风险存在的情况下做出选择。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Kevin P. Murphy：《Probabilistic Machine Learning》
* Mykel J. Kochenderfer：《Decision Making Under Uncertainty》

推荐教程 / 网课：

* Berkeley CS188 不确定性推理部分
* Probabilistic Graphical Models 相关课程
* Decision Making Under Uncertainty 相关课程
* 概率机器人 / 自动驾驶决策相关课程

对应项目：

* 电量不足时的任务选择
* 有障碍物风险时的路线选择
* 成功率和能耗权衡决策
* 根据置信度决定是否执行抓取
* 机器人风险决策系统

---

### 4.3 规则系统与专家系统

作用：

> 用明确规则实现可解释、可调试的决策逻辑，适合早期机器人系统和安全关键场景。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Peter Jackson：《Introduction to Expert Systems》
* Joseph C. Giarratano, Gary D. Riley：《Expert Systems: Principles and Programming》

推荐教程 / 网课：

* Expert Systems 教程
* Rule-Based AI 教程
* 机器人规则决策教程
* 嵌入式状态判断与规则控制教程

对应项目：

* 小车避障规则决策
* 低电量回充规则
* 安全急停规则
* 任务失败重试规则
* 无人机配送规则决策器

---

### 4.4 行为树

作用：

> 用树状结构组织机器人行为选择，适合复杂任务中的条件判断、行为切换和失败恢复。

推荐书籍：

* Michele Colledanchise, Petter Ögren：《Behavior Trees in Robotics and AI》
* Ian Millington：《Artificial Intelligence for Games》
* Mat Buckland：《Programming Game AI by Example》

推荐教程 / 网课：

* BehaviorTree.CPP 官方文档
* ROS 2 Navigation2 Behavior Trees 官方文档
* Behavior Trees for Robotics 相关教程
* Game AI Behavior Tree 教程

对应项目：

* 行为树机器人巡检系统
* 行为树导航失败恢复
* 行为树任务选择器
* 行为树组织导航、抓取、放置任务
* 修改 ROS 2 Navigation2 默认行为树

---

### 4.5 强化学习

作用：

> 让智能体通过与环境交互和奖励反馈，学习在不同状态下应该选择什么动作或策略。

推荐书籍：

* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Csaba Szepesvári：《Algorithms for Reinforcement Learning》
* Aske Plaat：《Deep Reinforcement Learning》

推荐教程 / 网课：

* David Silver Reinforcement Learning Course
* Hugging Face Deep RL Course
* Berkeley CS285: Deep Reinforcement Learning
* OpenAI Spinning Up
* Stable-Baselines3 官方文档

对应项目：

* DQN 网格世界智能体
* PPO 无人机配送任务
* 小车导航强化学习
* 机器人避障强化学习
* 基于奖励函数的任务决策策略

---

### 4.6 多智能体系统

作用：

> 让多个智能体之间能够协同、竞争、通信和分配任务。

推荐书籍：

* Michael Wooldridge：《An Introduction to MultiAgent Systems》
* Yoav Shoham, Kevin Leyton-Brown：《Multiagent Systems》
* Gerhard Weiss：《Multiagent Systems》

推荐教程 / 网课：

* Multi-Agent Systems 公开课
* Multi-Agent Reinforcement Learning 课程
* Berkeley / Stanford 多智能体相关课程
* 群体智能与多机器人系统课程

对应项目：

* 多机器人任务分配
* 多无人机协同配送
* 多智能体避障
* 多机器人区域覆盖
* 群体智能任务协作仿真

---

### 4.7 大语言模型智能体

作用：

> 使用 LLM 进行高层任务理解、技能选择、工具调用和自然语言决策辅助。

推荐书籍：

* Chip Huyen：《AI Engineering》
* Jay Alammar, Maarten Grootendorst：《Hands-On Large Language Models》
* Sebastian Raschka：《Build a Large Language Model From Scratch》

推荐教程 / 网课：

* LangChain Agents 官方文档
* LangGraph 官方文档
* OpenAI API 官方文档
* Hugging Face LLM Course
* DeepLearning.AI: AI Agents 相关课程

对应项目：

* LLM 选择机器人技能
* LLM 调用导航、检测、抓取工具
* 自然语言任务分解
* 机器人失败原因解释
* LLM + 规则系统的混合决策原型

---

### 4.8 技能库与工具调用

作用：

> 将机器人已有能力封装成可调用技能，让决策模块选择并调用合适的技能完成任务。

推荐书籍：

* Stuart Russell, Peter Norvig：《Artificial Intelligence: A Modern Approach》
* Chip Huyen：《AI Engineering》
* Martin Fowler：《Patterns of Enterprise Application Architecture》

推荐教程 / 网课：

* LangChain Tools 官方文档
* OpenAI Function Calling / Tool Calling 官方文档
* ROS 2 Actions 官方教程
* BehaviorTree.CPP 节点封装教程

对应项目：

* 封装机器人技能库
* 封装 navigate_to、detect_object、grasp_object、return_home 等技能
* 决策模块根据任务选择技能
* LLM 调用机器人技能
* 行为树调用机器人技能节点

---

## 5. 项目验证

### 5.1 入门项目：规则决策小车避障

目标：

```text id="gmhxjw"
用规则系统实现小车的基本避障决策。
```

示例规则：

```text id="83x1d7"
前方无障碍：继续前进
前方有障碍：停止
左侧空闲：左转
右侧空闲：右转
左右都阻挡：后退
```

验证能力：

```text id="vcz6w3"
能根据传感器状态选择行为
能写出可解释的决策逻辑
能让决策结果传给规划或控制模块
```

---

### 5.2 入门项目：低电量任务切换决策器

目标：

```text id="px0gfn"
当机器人电量不足时，自动切换到回充任务。
```

示例逻辑：

```text id="c2f6oh"
电量 > 40%：继续当前任务
20% < 电量 ≤ 40%：谨慎执行任务
电量 ≤ 20%：停止普通任务，切换到回充任务
```

验证能力：

```text id="8yfa0u"
能根据状态做任务切换
能处理任务优先级
能实现简单安全决策
```

---

### 5.3 进阶项目：行为树任务决策系统

目标：

```text id="45z7d3"
使用行为树组织机器人行为选择。
```

示例流程：

```text id="h891bq"
检查电量
→ 判断是否需要回充
→ 判断是否存在障碍物
→ 判断是否有任务目标
→ 执行导航 / 抓取 / 返回
```

验证能力：

```text id="1ee5g7"
能使用行为树表达决策逻辑
能处理失败恢复
能复用行为节点
能支持复杂任务流程
```

---

### 5.4 进阶项目：强化学习决策智能体

目标：

```text id="mfq5j4"
训练一个智能体根据环境状态选择动作。
```

可选任务：

```text id="1p4kv8"
网格世界寻路
无人机配送
小车避障
资源采集
自动回充
```

验证能力：

```text id="bvnxdw"
能定义状态、动作和奖励
能训练策略
能评估策略效果
能理解学习型决策和规则决策的区别
```

---

### 5.5 进阶项目：记忆驱动决策系统

目标：

```text id="86suah"
让历史经验影响当前决策。
```

示例流程：

```text id="v39sb4"
当前任务：前往厨房
记忆模块：厨房入口过去经常有障碍物
决策模块：提前减速，并请求规划模块选择备用路径
```

验证能力：

```text id="z0ezk0"
能调用历史经验
能根据失败案例调整当前策略
能让记忆模块真正参与决策
```

---

### 5.6 高级项目：LLM 技能选择 Agent

目标：

```text id="seyn3f"
让大语言模型根据任务选择机器人已有技能。
```

示例：

```text id="kb4ex6"
用户任务：
“去桌子附近找红色杯子。”

LLM 选择技能：
1. navigate_to(table)
2. detect_object(red_cup)
3. report_result()
```

验证能力：

```text id="l191et"
能将自然语言任务映射到技能库
能调用工具或函数
能生成高层决策序列
能和传统规则系统结合
```

---

### 5.7 高级项目：混合决策系统

目标：

```text id="wvx0k0"
结合规则决策、强化学习策略、记忆检索和安全约束，构建更可靠的决策系统。
```

示例结构：

```text id="8bvwie"
安全规则优先
↓
任务优先级判断
↓
历史经验检索
↓
规则决策 / RL 策略选择
↓
输出当前行为
```

验证能力：

```text id="gs5ylo"
能融合多种决策方式
能兼顾安全性、可解释性和学习能力
能用于真实或仿真机器人任务
```

---

## 6. 学习状态记录

| 知识点         | 当前状态 |
| ----------- | ---- |
| 人工智能导论      | 了解   |
| 决策理论与不确定性推理 | 未开始  |
| 规则系统与专家系统   | 了解   |
| 行为树         | 未开始  |
| 强化学习        | 入门   |
| 多智能体系统      | 了解   |
| 大语言模型智能体    | 了解   |
| 技能库与工具调用    | 未开始  |

状态标准：

```text id="n8ml4g"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

决策模块最终要实现：

```text id="cadlga"
智能体能够根据任务、状态、记忆和安全约束选择下一步行为；
能够在多个任务或技能之间进行选择；
能够在低电量、障碍物、失败、超时等情况下切换策略；
能够结合规则系统、行为树、强化学习和 LLM Agent 实现混合决策；
能够把决策结果传给规划模块或技能执行模块。
```

最终效果：

> 智能体不只是机械地执行固定流程，而是能够根据当前情况选择合适的行为，并在复杂环境中做出更合理、更安全、更可解释的决策。

