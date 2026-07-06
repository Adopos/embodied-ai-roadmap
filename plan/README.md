# 🤖 Embodied AI Full-Stack Roadmap (8-Week Intensive)

> **"软硬并行，知行合一。"** 本仓库基于具身智能 13 个核心模块架构，依托 **RTX 4060 笔记本 + STM32 单片机** 实现零成本纯仿真打法。通过“工具开路 + 数学内功 + 计算机底层 + 专业课分层”的四维并行模式，利用 8 周时间完成从神经末梢到顶层大脑的单点突破。

---

## 🧭 核心能力演进总览

| 阶段 | 周期 | 核心进化方向 | 覆盖知识树模块 | 核心沙盒环境 |
| :--- | :--- | :--- | :--- | :--- |
| **Phase 1** | W1 - W2 | 小脑发育与神经末梢 | `01`, `08`, `09`, `10` | Ubuntu 22.04 / Gazebo |
| **Phase 2** | W3 - W4 | 框架融合与空间感知 | `01`, `04`, `05`, `08`, `09` | ROS 2 Nav2 / OpenCV |
| **Phase 3** | W5 - W6 | AI 注入与边缘进化 | `01`, `05`, `07`, `11`, `12` | Hugging Face LeRobot / Isaac Lab |
| **Phase 4** | W7 - W8 | 顶层思维与防御安全 | `01`, `02`, `03`, `05`, `06`, `13` | VLM API / CBF Controller |

---

## 📅 8周魔鬼通关计划表

### 🟩 阶段一：工具开路与小脑运动学（W1 - W2）
#### 第 1 周：矩阵的艺术与底层驱动
* **🔧 工具课**：C++ 编程高级进阶与 CMake 构建系统（`01_Basic_capability_layer`）
    * *资源*：侯捷《C++面向对象高级开发》 / 《Effective C++》
* **🤖 专业课①**：STM32 固件开发与寄存器/HAL库应用（`01` & `10_Execution_module`）
    * *资源*：江科大自化协《STM32入门教程-基于HAL库》
* **🤖 专业课②**：机器人学运动学几何基础（`08_Planning_module`）
    * *资源*：台大林沛群《机器人学》 / 《Modern Robotics》
* **💻 🔀 核心内核（W1-W2）**：数据结构与算法
    * *资源*：普林斯顿《Algorithms》（算法第4版）
* **📐 🔀 数学内功（W1-W2）**：线性代数与矩阵空间
    * *资源*：MIT 18.06 *Linear Algebra* (Gilbert Strang)
* **🛠️ 本周实践**：
    - [ ] 用 CMake 构建 C++ 工程，手写 3 轴机械臂正运动学（FK）齐次变换矩阵。
    - [ ] 通过串口将计算出的角度发给 STM32，单片机解析并模拟输出 PWM 信号。

#### 第 2 周：经典控制 loop 与 Linux 家园
* **🔧 工具课**：Linux 操作系统内核使用与 Shell 脚本（`01_Basic_capability_layer`）
    * *资源*：《鸟哥的Linux私房菜》
* **🤖 专业课①**：经典控制理论与 PID 控制器算法（`09_Control_module`）
    * *资源*：Matlab 官方教程《Understanding PID Control》
* **🤖 专业课②**：机器人动力学与雅可比矩阵（`09_Control_module` & `10_Execution_module`）
    * *资源*：斯坦福 Oussama Khatib《Introduction to Robotics》(CS223A)
* **🛠️ 本周实践**：
    - [ ] 安装 Ubuntu 22.04 LTS 物理双系统。
    - [ ] 编写 Shell 脚本，一键编译并运行 C++ 机器人运动学/动力学求解代码。

---

### 🟨 阶段二：框架融合与睁眼看世界（W3 - W4）
#### 第 3 周：三维感知与分布式通信
* **🔧 工具课**：ROS 2 机器人操作系统（`01_Basic_capability_layer`）
    * *资源*：古月居《ROS 2入门21讲》 / 鱼香ROS 文档
* **🤖 专业课①**：计算机视觉与 YOLO 目标检测（`04_Perception_module`）
    * *资源*：吴恩达《Deep Learning》CNN 部分
* **🤖 专业课②**：三维 point cloud 处理与空间表示（`04_Perception_module` & `05_State&WorldModel_module`）
    * *资源*：深蓝学院《三维点云处理》
* **💻 🔀 核心内核（W3-W4）**：计算机操作系统（重点：线程调度、RTOS 硬实时）
    * *资源*：清华《操作系统》 / MIT 6.S081
* **📐 🔀 数学内功（W3-W4）**：概率论、数理统计与状态估计
    * *资源*：MIT 6.041 *Introduction to Probability* / DR_CAN 卡尔曼滤波
* **🛠️ 本周实践**：
    - [ ] 编写 ROS 2 C++ 节点调用笔记本摄像头，运行 YOLOv8 识别物体。
    - [ ] 结合相机内参矩阵，通过 ROS 2 Topic 发布物体在 3D 空间中的几何坐标。

#### 第 4 周：凸优化与自主定位建图
* **🔧 工具课**：Git 版本控制与 GitHub 协同开发（`01_Basic_capability_layer`）
* **🤖 专业课①**：经典路径规划算法与 ROS 2 Nav2 导航框架（`08_Planning_module`）
* **🤖 专业课②**：SLAM 导航建图与图优化理论（`04` & `05_State&WorldModel_module`）
    * *资源*：高翔《视觉SLAM十四讲：从理论到实践》
* **🛠️ 本周实践**：
    - [ ] 在 Gazebo 仿真中加载带雷达的虚拟小车，运行 Cartographer 进行房间建图。
    - [ ] 使用 Nav2 框架，利用 A* 算法控制小车在地图中自主避障导航。

---

### 🟦 阶段三：AI 注入与小脑进化（W5 - W6）
#### 第 5 周：模仿学习与端到端控制
* **🔧 工具课**：Python 高级编程与 PyTorch 深度学习框架（`01_Basic_capability_layer`）
    * *资源*：李沐《动手学深度学习》（PyTorch版）
* **🤖 专业课①**：深度学习基础网络（CNN/Transformer）原理（`12_Learning_module`）
* **🤖 专业课②**：模仿学习与 Diffusion Policy（`07_Decision_module` & `12_Learning_module`）
    * *资源*：Hugging Face 具身智能训练框架 **LeRobot**
* **💻 🔀 核心内核（W5-W6）**：计算机网络（重点：UDP、Socket编程与 DDS 通信）
    * *资源*：中科大郑烇《计算机网络》
* **📐 🔀 数学内功（W5-W6）**：凸优化理论
    * *资源*：斯坦福 Stephen Boyd *Convex Optimization*
* **🛠️ 本周实践**：
    - [ ] 在本地部署 LeRobot，调用 4060 显卡加载开源物理仿真数据集。
    - [ ] 训练基于 Diffusion Policy 的机械臂抓取网络，记录 Loss 收敛特征。

#### 第 6 周：大规模并行仿真与强化学习
* **🔧 工具课**：NVIDIA Isaac Lab / Omniverse 仿真开发（`01` & `05`）
    * *资源*：NVIDIA Isaac Lab 官方开发者指南
* **🤖 专业课①**：深度强化学习（DRL）算法 PPO / SAC（`11` & `12_Learning_module`）
    * *资源*：UC 伯克利 Sergey Levine *Deep RL (CS285)*
* **🤖 专业课②**：强化学习中的奖励函数设计与系统评估（`11_Feedback&Evaluation_module`）
* **🛠️ 本周实践**：
    - [ ] 部署 Isaac Lab，运行官方物理并行训练示例（如 `shadow_hand`）。
    - [ ] 开启 GPU 并行，利用 PPO 算法观测虚拟机器手在仿真空间中自我演化控球。

---

### 🟪 阶段四：顶层思维与安全闭环（W7 - W8）
#### 第 7 周：具身大模型与时序记忆
* **🔧 工具课**：大模型 API 接入与 Prompt 工程开发（`01` & `02_Interaction_module`）
* **🤖 专业课①**：大视觉语言模型（VLM）与具身大模型（RT-1/RT-2）架构（`02` & `03_Task_manage_module`）
    * *资源*：DeepMind *RT-2: Vision-Language-Action Models* 论文
* **🤖 专业课②**：机器人长期记忆与检索增强生成（`06_Memory_module`）
    * *资源*：斯坦福 *Voyager* 智能体 Skill Library 机制
* **💻 🔀 核心内核（W7-W8）**：计算机组成原理（重点：指令集、总线、多级缓存）
    * *资源*：哈工大刘宏伟《计算机组成原理》
* **📐 🔀 数学内功（W7-W8）**：动态规划与变分法
    * *资源*：MIT 6.252 *Dynamic Programming and Optimal Control*
* **🛠️ 本周实践**：
    - [ ] 编写 Python 脚本调用开源 VLM API，输入仿真截图与模糊自然语言指令。
    - [ ] 解析大模型返回的结构化 JSON 任务树，完成长程任务的第一步拆解。

#### 第 8 周：世界模型、防御性编程与数学防火墙（收官周）
* **🔧 工具课**：Linux/ROS 2 底层安全性配置与硬核防御性编程（`01` & `13`）
    * *资源*：《C++ 防御性编程指南》 / ROS 2 QoS 高级配置
* **🤖 专业课①**：世界模型（World Model）与视频生成式物理预测（`05_State&WorldModel_module`）
    * *资源*：马毅团队 / DeepMind GAIA-1 讲义
* **🤖 专业课②**：安全边界约束与硬性规则拦截控制 Safe-RL / CBF（`13_Safety_Constraint_module`）
    * *资源*：Control Barrier Functions (CBF) 学术讲义
* **🛠️ 本周实践**：
    - [ ] 编写 Python 版 CBF（安全屏障函数）控制器。
    - [ ] 模拟高风险场景：当神经网络意外输出暴冲指令时，CBF 防御代码能够在毫秒级强行拦截并将动作修正，确保物理安全。

---

## 🏁 终极里程碑：13 模块全链路总大整合（8周结束后开启）

当 8 周课程全部完成后，将开启单独的 **【大整合周】**。届时将拉通本仓库中的所有单点成果，实现**“数字孪生端到端长程任务闭环”**：
