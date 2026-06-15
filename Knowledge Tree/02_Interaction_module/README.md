# 02_交互模块

## 1. 模块定位

交互模块负责让具身智能体接收外部输入，并向人类、系统或其他智能体输出反馈信息。

它是智能体和外部世界之间的接口。

一句话概括：

> 交互模块负责“接收外部指令，并把指令转成智能体可以理解的任务输入”。

在完整具身智能体中，交互模块通常位于最前端：

```text
人类 / 系统 / 环境
        ↓
交互模块
        ↓
任务管理模块
        ↓
后续决策、规划、控制、执行
```

---

## 2. 模块输入

交互模块可能接收以下输入：

```text
自然语言指令
语音指令
按钮 / 遥控器输入
手机 App 指令
网页控制台指令
API 指令
传感器触发事件
人类反馈
其他智能体发送的信息
```

例子：

```text
“去桌子旁边找红色杯子”
“开始巡检”
“停止”
“返回充电”
“把这个任务标记为失败”
```

---

## 3. 模块输出

交互模块的输出不是直接控制电机，而是把外部输入转成系统可以理解的结构化信息。

常见输出：

```text
结构化任务语义
用户意图
任务参数
确认信息
状态反馈
失败说明
请求确认
```

例子：

```json
{
  "task_type": "find_object",
  "object": "red cup",
  "location": "table"
}
```

或者：

```json
{
  "task_type": "return_to_charger",
  "priority": "high"
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 自然语言处理

作用：

> 让智能体理解文字指令，把人类语言转成任务语义。

推荐书籍：

* Daniel Jurafsky, James H. Martin：《Speech and Language Processing》
* Jacob Eisenstein：《Introduction to Natural Language Processing》

推荐教程 / 网课：

* Stanford CS224N: Natural Language Processing with Deep Learning
* Hugging Face LLM Course
* Hugging Face Transformers Course

对应项目：

* 自然语言转结构化任务 JSON
* 从用户指令中提取任务类型、目标物体、位置和约束
* 构建简单任务解析器

---

### 4.2 语音识别

作用：

> 让智能体可以接收语音指令，而不是只能接收文字输入。

推荐书籍：

* Daniel Jurafsky, James H. Martin：《Speech and Language Processing》
* Lawrence Rabiner, Biing-Hwang Juang：《Fundamentals of Speech Recognition》

推荐教程 / 网课：

* Hugging Face Audio Course
* OpenAI Whisper 使用教程
* Coursera / edX 上的 Speech Recognition 相关课程

对应项目：

* 语音转文字
* 语音控制小车开始、停止、返回
* 语音输入任务后转成结构化任务

---

### 4.3 大语言模型应用

作用：

> 用 LLM 进行任务解析、任务改写、状态反馈、失败解释和工具调用。

推荐书籍：

* Sebastian Raschka：《Build a Large Language Model From Scratch》
* Chip Huyen：《AI Engineering》
* Jay Alammar, Maarten Grootendorst：《Hands-On Large Language Models》

推荐教程 / 网课：

* Hugging Face LLM Course
* OpenAI API 官方文档
* LangChain 官方文档
* DeepLearning.AI: ChatGPT Prompt Engineering for Developers

对应项目：

* LLM 将自然语言转成任务 JSON
* LLM 根据机器人状态生成自然语言反馈
* LLM 调用机器人已有技能
* 任务失败后自动生成失败说明

---

### 4.4 多模态大模型

作用：

> 让智能体结合图像、语言和环境信息进行交互。

推荐书籍：

* Paul Pu Liang 等：《Multimodal Machine Learning》
* 《Multimodal Deep Learning》

推荐教程 / 网课：

* CMU 11-777 Multimodal Machine Learning
* Hugging Face Vision-Language / Multimodal 相关教程
* LLaVA / CLIP / VLM 相关开源教程

对应项目：

* 输入图片和语言，判断用户要找的目标
* 根据摄像头画面回答环境问题
* 图像 + 语言生成结构化任务
* 为后续 VLA 模型打基础

---

### 4.5 人机交互

作用：

> 设计人与智能体之间的交互方式，让机器人更容易被控制、理解和调试。

推荐书籍：

* Alan Dix 等：《Human-Computer Interaction》
* Jenny Preece 等：《Interaction Design: Beyond Human-Computer Interaction》
* Don Norman：《The Design of Everyday Things》

推荐教程 / 网课：

* Georgia Tech CS6750: Human-Computer Interaction
* Coursera / edX Human-Computer Interaction 相关课程
* HCI + Robotics Interface 相关教程

对应项目：

* 设计一个机器人任务控制界面
* 显示机器人当前状态、电量、任务进度和失败原因
* 提供开始、暂停、取消、回充等操作按钮
* 设计适合机器人任务的交互流程

---

### 4.6 API 设计

作用：

> 让外部系统、网页、手机端或其他智能体可以通过接口控制机器人。

推荐书籍：

* Arnaud Lauret：《The Design of Web APIs》
* Leonard Richardson, Mike Amundsen, Sam Ruby：《RESTful Web APIs》

推荐教程 / 网课：

* FastAPI 官方教程
* REST API 设计教程
* OpenAPI / Swagger 教程
* WebSocket 实战教程

对应项目：

* 用 FastAPI 写机器人任务接口
* 外部系统通过 API 发送任务
* Web 控制台通过 API 控制机器人
* 提供查询机器人状态的接口

---

### 4.7 上位机界面开发

作用：

> 构建机器人控制台、监控界面和任务管理面板。

推荐书籍：

* Mark Lutz：《Programming Python》
* Alan D. Moore：《Python GUI Programming with Tkinter》
* Martin Fitzpatrick：《Create GUI Applications with Python & Qt》

推荐教程 / 网课：

* Streamlit 官方教程
* Gradio 官方教程
* PyQt / Qt for Python 官方教程
* Tkinter 官方教程

对应项目：

* 简单机器人控制面板
* 显示实时状态、电量、任务阶段
* 发送任务指令
* 查看任务日志和失败原因
* 可视化机器人运行状态

---

### 4.8 ROS 2 通信

作用：

> 让交互模块真正接入机器人系统，把外部任务传给 ROS 2 节点。

推荐书籍：

* Francisco Martín Rico：《A Concise Introduction to Robot Programming with ROS2》
* Lentin Joseph：《Robot Operating System for Absolute Beginners》

推荐教程 / 网课：

* ROS 2 官方 Tutorials
* The Construct ROS 2 课程
* 古月居 ROS 2 教程
* ROS 2 Topics / Services / Actions 官方文档

对应项目：

* 交互模块通过 ROS 2 Topic 发布任务
* 通过 ROS 2 Service 查询机器人状态
* 通过 ROS 2 Action 执行长时间任务
* Web 控制台和 ROS 2 机器人系统联动

---

## 5. 项目验证

### 5.1 入门项目：命令行任务输入

目标：

```text
通过命令行输入固定命令，让智能体执行对应任务。
```

示例命令：

```text
start
stop
go_to_charger
find_object
return_home
```

验证能力：

```text
能接收外部输入
能解析简单命令
能把命令传给任务管理模块
```

---

### 5.2 进阶项目：自然语言转结构化任务

目标：

```text
输入自然语言，输出结构化任务 JSON。
```

示例：

```text
输入：
“去桌子旁边找红色杯子。”

输出：
{
  "task_type": "find_object",
  "object": "red cup",
  "location": "table"
}
```

验证能力：

```text
能理解自然语言任务
能提取任务类型、目标物体、位置等参数
能把自然语言任务转成系统可执行格式
```

---

### 5.3 进阶项目：Web 控制台控制机器人

目标：

```text
通过网页界面发送任务指令，并显示机器人当前状态。
```

功能：

```text
发送任务
暂停任务
取消任务
查看当前状态
查看任务结果
查看失败原因
```

验证能力：

```text
能设计简单人机交互界面
能通过 API 和机器人系统通信
能显示任务状态和反馈信息
```

---

### 5.4 高级项目：语言驱动机器人技能调用

目标：

```text
用户输入自然语言，系统解析任务并调用已有机器人技能。
```

示例：

```text
用户：
“去桌子附近找红色物体。”

系统调用：
1. navigate_to(table)
2. detect_object(red_object)
3. report_result()
```

验证能力：

```text
能将语言指令映射到机器人技能
能和任务管理、决策、规划模块联动
能在失败时向用户反馈原因
```

---

## 6. 学习状态记录

| 知识点      | 当前状态 |
| -------- | ---- |
| 自然语言处理   | 未开始  |
| 语音识别     | 未开始  |
| 大语言模型应用  | 未开始   |
| 多模态大模型   | 未开始   |
| 人机交互     | 未开始  |
| API 设计   | 未开始  |
| 上位机界面开发  | 未开始  |
| ROS 2 通信 | 未开始  |

状态标准：

```text
未开始
了解
入门
能做小项目
能讲清楚
能写进简历
```

---

## 7. 本模块最终目标

交互模块最终要实现：

```text
人类可以通过语言、语音、界面或 API 给智能体下达任务；
智能体可以把任务解析成结构化形式；
智能体可以在执行过程中反馈状态；
智能体可以在失败时说明原因并请求帮助。
```

最终效果：

> 机器人不只是被代码控制，而是能通过自然交互接收任务、报告状态、请求确认和解释失败原因。
