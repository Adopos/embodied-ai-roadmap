# 12_学习模块

## 1. 模块定位

学习模块负责让具身智能体通过数据、奖励、示范、反馈和历史经验不断提升能力。

它回答的问题是：

> 智能体如何从经验中变强？如何通过训练提升感知、决策、规划、控制和执行能力？

学习模块不是单纯“训练一个模型”。
在具身智能体中，学习模块可以更新很多部分：

```text id="lfn1lq"
感知模型
决策策略
控制策略
世界模型
记忆系统
任务经验
规划偏好
失败恢复策略
```

一句话概括：

> 学习模块负责“让智能体通过经验、数据和反馈持续改进”。

在完整具身智能体中，学习模块通常接收反馈评价模块和记忆模块的数据，并反向更新其他模块：

```text id="j0h9kk"
反馈评价模块
记忆模块
历史数据
专家示范
        ↓
学习模块
        ↓
更新感知、决策、规划、控制、记忆、世界模型
```

---

## 2. 模块输入

学习模块可能接收以下输入：

```text id="6r3sli"
任务反馈
奖励信号
成功轨迹
失败轨迹
专家示范
遥操作数据
机器人传感器数据
机器人状态数据
历史任务经验
人类反馈
仿真数据
真实机器人数据
训练日志
实验评估结果
```

例子：

```text id="43k3vv"
无人机配送任务的奖励
机械臂抓取成功或失败数据
人类遥操作机械臂的轨迹
小车导航过程中的状态和动作
机器人碰撞失败案例
仿真环境中的训练数据
真实机器人采集的数据集
```

---

## 3. 模块输出

学习模块的输出是被更新后的模型、策略、经验或参数。

常见输出：

```text id="fvsz49"
感知模型
策略模型
控制策略
动作预测模型
世界模型
任务经验库
失败经验
模型参数
训练曲线
评估结果
优化后的奖励函数
更新后的决策规则
```

例子：

```json id="86v89n"
{
  "model_type": "policy",
  "algorithm": "PPO",
  "task": "drone_delivery",
  "average_reward": 850,
  "success_rate": 0.72
}
```

或者：

```json id="n294zl"
{
  "model_type": "imitation_policy",
  "task": "robot_arm_pick_place",
  "dataset": "teleoperation_demos",
  "success_rate": 0.65
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 机器学习

作用：

> 建立模型训练、数据划分、泛化、评估和优化的基础，是所有学习型智能体的底层知识。

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

* 监督学习分类项目
* 回归预测项目
* 模型训练与评估实验
* 机器人传感器数据分类
* 任务成功率预测模型

---

### 4.2 深度学习

作用：

> 使用神经网络从图像、状态、语言、动作和轨迹数据中学习复杂表示和策略。

推荐书籍：

* Ian Goodfellow, Yoshua Bengio, Aaron Courville：《Deep Learning》
* Aston Zhang 等：《Dive into Deep Learning》
* Michael Nielsen：《Neural Networks and Deep Learning》

推荐教程 / 网课：

* MIT 6.S191: Introduction to Deep Learning
* Stanford CS231n: Deep Learning for Computer Vision
* Dive into Deep Learning 官方教程
* PyTorch 官方教程

对应项目：

* PyTorch 图像分类
* 机器人状态预测模型
* 视觉特征提取模型
* 动作预测网络
* 简单策略网络训练

---

### 4.3 强化学习

作用：

> 让智能体通过与环境交互、获得奖励和试错，学习在不同状态下应该采取什么动作。

推荐书籍：

* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Csaba Szepesvári：《Algorithms for Reinforcement Learning》
* Dimitri P. Bertsekas：《Reinforcement Learning and Optimal Control》

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
* 自动回充策略学习
* 强化学习训练曲线分析

---

### 4.4 模仿学习

作用：

> 让智能体从人类示范、专家轨迹或遥操作数据中学习动作策略，适合机器人抓取、放置、操作和导航任务。

推荐书籍：

* Stephane Ross 等模仿学习相关教材与讲义
* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Ian Goodfellow 等：《Deep Learning》

推荐教程 / 网课：

* LeRobot 官方文档
* LeRobot Imitation Learning on Real-World Robots 教程
* Stanford CS234 / CS285 相关模仿学习内容
* Isaac Lab Imitation Learning 教程
* ManiSkill Learning from Demonstrations 教程

对应项目：

* Behavior Cloning 专家轨迹学习
* 人类遥操作数据采集
* LeRobot 机械臂模仿学习
* 机械臂抓取和放置任务
* 小车跟随专家轨迹
* 从成功轨迹中学习动作策略

---

### 4.5 离线强化学习

作用：

> 让智能体在固定数据集上学习策略，而不是必须实时和环境交互，适合机器人历史数据和昂贵真实环境训练。

推荐书籍：

* Sergey Levine 等离线强化学习讲义
* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Dimitri P. Bertsekas：《Reinforcement Learning and Optimal Control》

推荐教程 / 网课：

* Berkeley CS285 离线强化学习相关内容
* Offline Reinforcement Learning 公开课
* D4RL 相关教程
* Decision Transformer 教程
* IQL / CQL / TD3+BC 开源教程

对应项目：

* 使用固定轨迹数据训练策略
* 离线小车导航策略学习
* 离线机械臂抓取策略学习
* Decision Transformer 小实验
* 比较在线 RL 与离线 RL 的差异
* 从历史失败和成功数据中学习策略

---

### 4.6 机器人学习

作用：

> 将机器学习、强化学习、模仿学习和机器人系统结合起来，让机器人通过数据和经验学习具体技能。

推荐书籍：

* Bruno Siciliano 等：《Robotics: Modelling, Planning and Control》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics: Mechanics, Planning, and Control》
* Jan Peters, Sethu Vijayakumar, Stefan Schaal 等机器人学习相关资料

推荐教程 / 网课：

* LeRobot 官方文档
* ManiSkill 官方文档
* Isaac Lab 官方文档
* Berkeley CS285: Deep Reinforcement Learning
* Stanford CS123 / CS224R / Robotics Learning 相关课程

对应项目：

* LeRobot 机械臂学习
* ManiSkill 抓取任务训练
* Isaac Lab 机器人控制训练
* 机械臂从示范中学习抓取
* 移动机器人从奖励中学习导航
* 机器人策略训练与评估完整流程

---

### 4.7 自监督学习与表征学习

作用：

> 让智能体从大量无标签数据中学习有用表示，为视觉、状态表示、世界模型和机器人学习打基础。

推荐书籍：

* Ian Goodfellow, Yoshua Bengio, Aaron Courville：《Deep Learning》
* Kevin P. Murphy：《Probabilistic Machine Learning》
* Aston Zhang 等：《Dive into Deep Learning》

推荐教程 / 网课：

* Stanford CS231n 表征学习相关内容
* DeepLearning.AI 自监督学习相关课程
* Hugging Face Computer Vision / Transformers 教程
* 对比学习、Masked Modeling、Representation Learning 相关公开课

对应项目：

* 视觉表征学习小实验
* 机器人状态编码器
* 图像对比学习实验
* 视频预测前置表示学习
* 用预训练视觉特征辅助机器人决策
* 为世界模型学习潜在状态表示

---

### 4.8 世界模型与模型化强化学习

作用：

> 学习环境动态，预测未来状态，让智能体可以在内部模型中进行推演、规划和策略优化。

推荐书籍：

* Richard S. Sutton, Andrew G. Barto：《Reinforcement Learning: An Introduction》
* Kevin P. Murphy：《Probabilistic Machine Learning》
* Dimitri P. Bertsekas：《Dynamic Programming and Optimal Control》

推荐教程 / 网课：

* Model-Based Reinforcement Learning 公开课
* Dreamer / World Models 相关教程
* David Silver Reinforcement Learning Course
* Berkeley CS285 Model-Based RL 相关内容
* Hugging Face Deep RL Course 相关内容

对应项目：

* 网格世界状态预测模型
* 无人机配送下一状态预测
* 简单 Model-Based RL 实验
* Dreamer 小实验
* 学习环境动态模型
* 用世界模型辅助规划和决策

---

### 4.9 生成式策略学习

作用：

> 使用生成模型学习动作序列，适合复杂机器人操作任务，例如机械臂抓取、放置、推拉和长序列动作生成。

推荐书籍：

* Ian Goodfellow 等：《Deep Learning》
* Kevin P. Murphy：《Probabilistic Machine Learning》
* Jay Alammar, Maarten Grootendorst：《Hands-On Large Language Models》

推荐教程 / 网课：

* Diffusion Policy 官方论文与开源教程
* ManiSkill Diffusion Policy 相关教程
* LeRobot Policy 相关教程
* Generative Models 公开课
* Hugging Face Diffusion Models Course

对应项目：

* Diffusion Policy 入门实验
* 机械臂抓取动作序列生成
* 从遥操作数据学习动作分布
* ManiSkill 中训练生成式策略
* LeRobot 中使用策略模型完成操作任务

---

### 4.10 持续学习

作用：

> 让智能体在长期运行中学习新任务，同时尽量避免遗忘旧任务。

推荐书籍：

* German I. Parisi 等持续学习综述与教材资料
* Ian Goodfellow 等：《Deep Learning》
* Kevin P. Murphy：《Probabilistic Machine Learning》

推荐教程 / 网课：

* Continual Learning 公开课
* Avalanche 官方文档
* ContinualAI 教程
* Lifelong Learning / Continual Learning 相关课程
* Online Learning 相关课程

对应项目：

* 多任务顺序学习实验
* 机器人学习新任务后保持旧任务能力
* 任务经验回放
* 防止策略灾难性遗忘
* 长期任务经验更新系统

---

### 4.11 Sim2Real 与迁移学习

作用：

> 将仿真中学到的策略迁移到真实机器人中，减少真实环境试错成本。

推荐书籍：

* Ian Goodfellow 等：《Deep Learning》
* Kevin M. Lynch, Frank C. Park：《Modern Robotics》
* Roland Siegwart 等：《Introduction to Autonomous Mobile Robots》

推荐教程 / 网课：

* Isaac Lab Sim2Real 教程
* ManiSkill Sim2Real 相关教程
* Domain Randomization 教程
* Robot Learning Sim2Real 公开课
* Transfer Learning 相关课程

对应项目：

* 仿真小车策略迁移
* 仿真机械臂抓取策略迁移
* 域随机化实验
* 仿真与真实环境性能对比
* AirSim 训练策略迁移到真实无人机思路验证

---

## 5. 项目验证

### 5.1 入门项目：DQN / PPO 网格世界智能体

目标：

```text id="oxcr2f"
训练一个智能体在简单二维环境中完成任务。
```

任务示例：

```text id="whlmur"
寻找能量
躲避障碍
回到基地
到达目标点
```

验证能力：

```text id="senghb"
能定义状态、动作和奖励
能训练基础 RL agent
能分析训练曲线
能理解学习模块如何通过反馈改进策略
```

---

### 5.2 入门项目：PyTorch 策略网络

目标：

```text id="vn6pr3"
使用 PyTorch 构建一个简单策略网络或动作预测网络。
```

功能：

```text id="n7m7v3"
输入状态
输出动作概率或动作值
计算损失
反向传播
更新参数
```

验证能力：

```text id="tmfh36"
能理解神经网络策略
能把深度学习和智能体动作选择联系起来
```

---

### 5.3 进阶项目：PPO 无人机配送任务

目标：

```text id="o92aos"
在无人机配送环境中训练 PPO 策略。
```

任务内容：

```text id="pz7mvb"
取货
送货
避障
充电
返回
提升平均回报
降低碰撞率
提高投递成功数
```

验证能力：

```text id="h4y18c"
能将强化学习用于具身智能任务
能设计奖励函数
能分析策略表现
能和已有无人机 RL 项目形成连接
```

---

### 5.4 进阶项目：Behavior Cloning 专家轨迹学习

目标：

```text id="m4jyjy"
让智能体从专家轨迹中学习动作。
```

数据形式：

```text id="8id4j7"
状态
动作
图像
关节角
末端位姿
任务标签
```

验证能力：

```text id="b4k19m"
能理解模仿学习
能采集或使用专家数据
能训练动作预测模型
能比较专家策略和学习策略
```

---

### 5.5 进阶项目：LeRobot 机械臂模仿学习

目标：

```text id="eyjz12"
使用 LeRobot 完成一个机械臂模仿学习任务。
```

任务示例：

```text id="xipxoz"
抓取物体
放入盒子
推动物体
整理桌面
简单 pick-and-place
```

验证能力：

```text id="f98d1a"
能采集遥操作数据
能训练机器人策略
能评估真实或仿真机器人成功率
能理解机器人学习完整流程
```

---

### 5.6 进阶项目：ManiSkill 抓取任务训练

目标：

```text id="rn4hqf"
在 ManiSkill 中训练机器人完成抓取或操作任务。
```

可选方法：

```text id="v5j4ln"
强化学习
模仿学习
Behavior Cloning
Diffusion Policy
预训练策略评估
```

验证能力：

```text id="3vxgy6"
能使用机器人学习仿真平台
能训练或评估策略
能比较不同学习方法的效果
```

---

### 5.7 高级项目：Diffusion Policy 入门实验

目标：

```text id="5940fp"
使用生成式策略学习机器人动作序列。
```

任务内容：

```text id="ij7021"
读取示范数据
训练动作生成模型
输入当前观测
生成未来动作序列
执行并评估成功率
```

验证能力：

```text id="030c6t"
能理解生成式策略学习
能将扩散模型用于机器人动作生成
能为 VLA 和机器人基础模型打基础
```

---

### 5.8 高级项目：世界模型小实验

目标：

```text id="swjtwf"
训练模型预测环境下一步状态，并用于辅助决策或规划。
```

输入输出：

```text id="0lm09e"
输入：当前状态 + 动作
输出：下一步状态预测
```

验证能力：

```text id="00j89y"
能理解世界模型的基本作用
能将状态预测和决策联系起来
能为 Model-Based RL 打基础
```

---

### 5.9 高级项目：机器人学习完整闭环

目标：

```text id="al1cql"
构建一个从数据采集、模型训练、策略评估到失败分析的完整机器人学习流程。
```

完整流程：

```text id="tfebia"
采集数据
清洗数据
训练模型
评估策略
记录指标
分析失败案例
更新数据集
重新训练
```

验证能力：

```text id="febljn"
能把学习模块和感知、状态、决策、控制、反馈、记忆模块连接起来
能形成真正可迭代的具身智能学习系统
```

---

## 6. 学习状态记录

| 知识点            | 当前状态 |
| -------------- | ---- |
| 机器学习           | 入门   |
| 深度学习           | 入门   |
| 强化学习           | 入门   |
| 模仿学习           | 未开始  |
| 离线强化学习         | 未开始  |
| 机器人学习          | 了解   |
| 自监督学习与表征学习     | 未开始  |
| 世界模型与模型化强化学习   | 了解   |
| 生成式策略学习        | 未开始  |
| 持续学习           | 了解   |
| Sim2Real 与迁移学习 | 未开始  |

状态标准：

```text id="zojc1g"
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

学习模块最终要实现：

```text id="bkr1tj"
智能体能够从奖励中学习策略；
能够从专家示范中学习动作；
能够从历史数据中离线学习；
能够从大量无标签数据中学习表示；
能够通过世界模型预测未来状态；
能够在仿真和真实环境之间迁移策略；
能够根据反馈评价结果持续改进；
能够让感知、决策、规划、控制和记忆模块不断变强。
```

最终效果：

> 智能体不只是执行固定程序，而是能够通过数据、反馈、奖励和示范不断学习，在长期运行中逐渐提升任务完成能力。

