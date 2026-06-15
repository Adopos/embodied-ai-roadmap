# 01_基础能力层

## 1. 模块定位

基础能力层不是具身智能体中的某一个功能模块，而是支撑所有模块的底层能力。

它回答的问题是：

> 想要真正理解并构建具身智能体，需要哪些数学、编程、AI 和工程基础？

基础能力层会支撑以下所有模块：

```text id="tokluu"
交互模块
任务管理模块
感知模块
状态 / 世界模型模块
记忆模块
决策模块
规划模块
控制模块
执行模块
反馈评价模块
学习模块
安全约束模块
```

一句话概括：

> 基础能力层负责“为构建具身智能体提供数学、编程、AI 和工程底座”。

---

## 2. 基础能力层的作用

具身智能体不是单一模型，而是一个复杂系统。

它需要：

```text id="dks4om"
数学基础
编程能力
算法能力
AI 基础
工程能力
实验能力
文档能力
```

如果基础能力不够，后面学习机器人学、SLAM、强化学习、控制、视觉、ROS 2 和硬件系统都会很吃力。

---

## 3. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 3.1 微积分

作用：

> 理解变化率、连续变化、优化、运动、控制和机器学习中的函数变化。

推荐书籍：

* James Stewart：《Calculus》
* Thomas：《Thomas' Calculus》
* 同济大学：《高等数学》

推荐教程 / 网课：

* MIT OCW 18.01 Single Variable Calculus
* MIT OCW 18.02 Multivariable Calculus
* Khan Academy Calculus
* 中国大学 MOOC 高等数学课程
* B站高等数学系统课程

对应项目：

* 机器人运动过程中的速度、加速度理解
* 梯度下降可视化实验
* 神经网络损失函数变化分析
* 控制系统中连续变化量理解

---

### 3.2 线性代数

作用：

> 理解向量、矩阵、坐标变换、神经网络、机器人位姿、SLAM 和三维空间计算。

推荐书籍：

* Gilbert Strang：《Introduction to Linear Algebra》
* David C. Lay：《Linear Algebra and Its Applications》
* 同济大学：《线性代数》

推荐教程 / 网课：

* MIT OCW 18.06 Linear Algebra
* 3Blue1Brown: Essence of Linear Algebra
* Khan Academy Linear Algebra
* 中国大学 MOOC 线性代数课程
* B站线性代数系统课程

对应项目：

* 二维 / 三维坐标变换实验
* 机器人位姿矩阵表示
* 图像矩阵处理
* 神经网络前向传播矩阵计算
* PCA 降维小实验

---

### 3.3 概率论与数理统计

作用：

> 理解不确定性、噪声、估计、采样、强化学习、机器学习评估和机器人状态估计。

推荐书籍：

* Sheldon Ross：《A First Course in Probability》
* Joseph K. Blitzstein, Jessica Hwang：《Introduction to Probability》
* 陈希孺：《概率论与数理统计》
* 浙江大学：《概率论与数理统计》

推荐教程 / 网课：

* MIT OCW 18.05 Introduction to Probability and Statistics
* Harvard STAT 110
* Khan Academy Statistics and Probability
* 中国大学 MOOC 概率论与数理统计课程
* B站概率论系统课程

对应项目：

* 传感器噪声建模
* 机器人定位不确定性理解
* 强化学习随机策略实验
* 机器学习模型评估统计
* 蒙特卡洛模拟小实验

---

### 3.4 最优化方法

作用：

> 理解机器学习训练、轨迹优化、控制优化、路径规划和模型参数更新。

推荐书籍：

* Stephen Boyd, Lieven Vandenberghe：《Convex Optimization》
* Jorge Nocedal, Stephen Wright：《Numerical Optimization》
* Dimitri P. Bertsekas：《Nonlinear Programming》

推荐教程 / 网课：

* Stanford Convex Optimization
* Boyd Convex Optimization 公开资料
* MIT Optimization Methods 相关课程
* Convex Optimization 公开课
* CVXPY 官方教程

对应项目：

* 梯度下降实验
* 线性回归参数优化
* 轨迹优化小实验
* 约束条件下路径优化
* 机器人控制中的优化问题理解

---

### 3.5 离散数学

作用：

> 理解图、集合、逻辑、关系、状态机、搜索、规划和计算机科学基础。

推荐书籍：

* Kenneth H. Rosen：《Discrete Mathematics and Its Applications》
* Susanna S. Epp：《Discrete Mathematics with Applications》
* Seymour Lipschutz：《Discrete Mathematics》

推荐教程 / 网课：

* MIT OCW Mathematics for Computer Science
* Berkeley CS70
* 中国大学 MOOC 离散数学课程
* B站离散数学系统课程
* Discrete Mathematics 公开课

对应项目：

* 图搜索算法实验
* 状态机建模
* 任务依赖图
* 路径规划中的图表示
* 行为树和任务图理解

---

### 3.6 数据结构与算法

作用：

> 支撑路径规划、任务搜索、图搜索、数据处理、系统开发和高效编程。

推荐书籍：

* Thomas H. Cormen 等：《Introduction to Algorithms》
* Robert Sedgewick, Kevin Wayne：《Algorithms》
* 邓俊辉：《数据结构》

推荐教程 / 网课：

* MIT OCW 6.006 Introduction to Algorithms
* Princeton Algorithms
* UC Berkeley CS61B
* 中国大学 MOOC 数据结构与算法课程
* LeetCode / 代码随想录

对应项目：

* BFS / DFS 路径搜索
* Dijkstra / A* 路径规划
* 优先队列任务调度
* 地图图结构表示
* 机器人任务队列管理

---

### 3.7 Python 程序设计

作用：

> 用于 AI 训练、数据处理、仿真环境、机器人原型开发、实验分析和自动化脚本。

推荐书籍：

* Mark Lutz：《Learning Python》
* Eric Matthes：《Python Crash Course》
* Al Sweigart：《Automate the Boring Stuff with Python》

推荐教程 / 网课：

* Python 官方教程
* CS50P: Introduction to Programming with Python
* Real Python 教程
* 廖雪峰 Python 教程
* 菜鸟教程 Python

对应项目：

* Python 基础练习
* 数据处理脚本
* 仿真环境控制脚本
* 强化学习训练脚本
* 实验结果可视化脚本

---

### 3.8 C / C++ 程序设计

作用：

> 用于嵌入式开发、ROS 2、机器人底层控制、实时系统和高性能模块开发。

推荐书籍：

* Bjarne Stroustrup：《Programming: Principles and Practice Using C++》
* Stanley B. Lippman：《C++ Primer》
* K. N. King：《C Programming: A Modern Approach》

推荐教程 / 网课：

* LearnCpp
* MIT 6.096 Introduction to C++
* CS50 C 语言部分
* 中国大学 MOOC C / C++ 程序设计课程
* B站 C / C++ 系统课程

对应项目：

* C 语言基础练习
* C++ 类与对象实验
* 简单机器人状态机
* ROS 2 C++ 节点
* STM32 C 语言控制程序

---

### 3.9 Linux

作用：

> 支撑 ROS 2、机器人开发环境、服务器训练、驱动安装、终端操作和工程部署。

推荐书籍：

* William Shotts：《The Linux Command Line》
* Brian Ward：《How Linux Works》
* Mark Sobell：《A Practical Guide to Linux Commands, Editors, and Shell Programming》

推荐教程 / 网课：

* Linux Journey
* MIT Missing Semester
* The Linux Command Line 官方资料
* 鸟哥的 Linux 私房菜
* B站 Linux 系统课程

对应项目：

* Linux 命令行基础
* Conda / Python 环境管理
* ROS 2 环境配置
* 服务器训练环境配置
* Shell 脚本自动化实验

---

### 3.10 Git / GitHub

作用：

> 用于代码版本管理、项目沉淀、实验记录、作品集展示和协作开发。

推荐书籍：

* Scott Chacon, Ben Straub：《Pro Git》
* Jon Loeliger, Matthew McCullough：《Version Control with Git》
* Emma Jane Hogbin Westby：《Git for Teams》

推荐教程 / 网课：

* Pro Git 官方在线书
* Git 官方文档
* GitHub Docs
* Atlassian Git Tutorials
* 廖雪峰 Git 教程

对应项目：

* 建立 embodied-ai-roadmap 仓库
* 使用 Git 提交每日学习记录
* 管理无人机 RL 项目版本
* 写 GitHub README
* 用 Issues 记录问题和改进

---

### 3.11 计算机系统基础

作用：

> 理解程序如何运行、内存如何管理、操作系统如何调度任务，是深入工程开发和机器人系统部署的重要基础。

推荐书籍：

* Randal E. Bryant, David R. O’Hallaron：《Computer Systems: A Programmer's Perspective》
* Abraham Silberschatz 等：《Operating System Concepts》
* Remzi H. Arpaci-Dusseau, Andrea C. Arpaci-Dusseau：《Operating Systems: Three Easy Pieces》

推荐教程 / 网课：

* CMU 15-213: Introduction to Computer Systems
* MIT 6.S081 Operating System Engineering
* Berkeley CS162 Operating Systems
* 南京大学操作系统课程
* 哈工大操作系统课程

对应项目：

* 理解程序编译和运行
* 进程与线程实验
* Linux 进程管理
* 简单多线程任务调度
* 机器人多模块程序运行理解

---

### 3.12 机器学习

作用：

> 理解数据、模型、训练、泛化和评估，是感知、预测、决策和学习模块的基础。

推荐书籍：

* Christopher M. Bishop：《Pattern Recognition and Machine Learning》
* Trevor Hastie, Robert Tibshirani, Jerome Friedman：《The Elements of Statistical Learning》
* Aurélien Géron：《Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow》

推荐教程 / 网课：

* Stanford CS229: Machine Learning
* Coursera Machine Learning Specialization
* Google Machine Learning Crash Course
* scikit-learn 官方教程

对应项目：

* 分类模型训练
* 回归模型训练
* 任务成功率预测
* 传感器数据分类
* 机器学习模型评估实验

---

### 3.13 深度学习 / PyTorch

作用：

> 支撑计算机视觉、强化学习、模仿学习、多模态模型、VLA 和机器人学习。

推荐书籍：

* Ian Goodfellow, Yoshua Bengio, Aaron Courville：《Deep Learning》
* Aston Zhang 等：《Dive into Deep Learning》
* Michael Nielsen：《Neural Networks and Deep Learning》

推荐教程 / 网课：

* MIT 6.S191: Introduction to Deep Learning
* Stanford CS231n
* Dive into Deep Learning 官方教程
* PyTorch 官方教程
* Hugging Face 深度学习相关教程

对应项目：

* PyTorch 图像分类
* MLP / CNN / RNN / Transformer 小实验
* 强化学习策略网络
* 机器人状态预测网络
* 视觉模型训练实验

---

### 3.14 工程文档写作

作用：

> 将学习过程、项目结构、实验结果和失败经验沉淀成 GitHub 文档、实验报告、技术博客和简历素材。

推荐书籍：

* Joshua Schimel：《Writing Science》
* Robert A. Day, Barbara Gastel：《How to Write and Publish a Scientific Paper》
* Alley Michael：《The Craft of Scientific Writing》
* Gerald J. Alred 等：《Handbook of Technical Writing》

推荐教程 / 网课：

* Coursera Writing in the Sciences
* MIT / Stanford 科研写作相关课程
* Google Technical Writing Courses
* GitHub README 写作教程
* Atlassian 技术文档教程

对应项目：

* 写 GitHub 项目 README
* 写无人机 RL 项目文档
* 写电赛控制项目报告
* 写实验复盘文档
* 整理简历项目素材

---

## 4. 项目验证

### 4.1 GitHub 知识树仓库

目标：

```text id="rre4ha"
建立并持续维护 embodied-ai-roadmap 仓库。
```

内容：

```text id="j0wf95"
具身智能体知识树
每个模块 README
学习资源记录
项目验证记录
每周复盘
```

验证能力：

```text id="oh9ssz"
能使用 GitHub 管理长期学习
能把知识体系沉淀成作品
能形成可展示的个人成长路线
```

---

### 4.2 Python 数据处理与可视化项目

目标：

```text id="nv9dfe"
使用 Python 处理实验数据并绘制图表。
```

内容：

```text id="tdtno5"
读取 CSV / JSON
清洗数据
统计指标
绘制曲线
生成实验结果图
```

验证能力：

```text id="xhnt0t"
能处理项目实验数据
能分析训练曲线
能支撑反馈评价模块
```

---

### 4.3 PyTorch 基础模型训练项目

目标：

```text id="ewcm00"
使用 PyTorch 完成一个基础模型训练流程。
```

内容：

```text id="91rqj9"
准备数据集
构建模型
定义损失函数
训练模型
评估模型
保存模型
```

验证能力：

```text id="8m7kc7"
能掌握深度学习训练流程
能为后续感知、强化学习、模仿学习打基础
```

---

### 4.4 算法与路径搜索小项目

目标：

```text id="i0h9jf"
用数据结构与算法实现基础路径搜索。
```

内容：

```text id="linlxc"
二维网格地图
BFS
Dijkstra
A*
路径可视化
障碍物设置
```

验证能力：

```text id="glq0pk"
能把算法知识用到机器人路径规划
能为规划模块打基础
```

---

### 4.5 Linux + Git + Python 工程环境

目标：

```text id="zq4qk5"
建立基本机器人与 AI 开发环境。
```

内容：

```text id="zbdv60"
Linux 命令行
Conda 环境
Git 版本管理
Python 项目结构
VS Code
依赖管理
```

验证能力：

```text id="qtqbei"
能独立配置开发环境
能运行 AI / 机器人项目
能管理代码和实验版本
```

---

### 4.6 基础 AI 小实验合集

目标：

```text id="ixhloq"
完成一组机器学习和深度学习基础实验。
```

内容：

```text id="vnkkbv"
线性回归
逻辑回归
MLP
CNN
简单 Transformer
模型评估
训练曲线分析
```

验证能力：

```text id="rc7ieu"
能理解 AI 模型训练流程
能为感知模块和学习模块打基础
```

---

## 5. 学习状态记录

| 知识点            | 当前状态 |
| -------------- | ---- |
| 微积分            | 入门   |
| 线性代数           | 入门   |
| 概率论与数理统计       | 入门   |
| 最优化方法          | 未开始  |
| 离散数学           | 未开始  |
| 数据结构与算法        | 入门   |
| Python 程序设计    | 入门   |
| C / C++ 程序设计   | 入门   |
| Linux          | 未开始  |
| Git / GitHub   | 入门   |
| 计算机系统基础        | 入门   |
| 机器学习           | 入门   |
| 深度学习 / PyTorch | 入门   |
| 工程文档写作         | 入门   |

状态标准：

```text id="nvofem"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 6. 本模块最终目标

基础能力层最终要实现：

```text id="itvofp"
能够理解具身智能相关数学基础；
能够使用 Python 和 C / C++ 编写基础程序；
能够使用 Linux 和 GitHub 管理开发环境和项目；
能够掌握机器学习和深度学习基本流程；
能够完成基础算法、数据处理和模型训练实验；
能够把学习过程、项目过程和实验结果写成清晰文档；
能够为后续感知、状态、决策、规划、控制、执行、学习等模块打下基础。
```

最终效果：

> 具身智能的学习不是从前沿论文直接开始，而是先建立稳定的数学、编程、AI 和工程底座，再逐步进入机器人系统和具身智能前沿。

