# 04_感知模块

## 1. 模块定位

感知模块负责让具身智能体从传感器中获取外部世界信息。

它回答的问题是：

> 智能体看到了什么？周围有什么？目标在哪里？环境中有哪些障碍物？

在完整具身智能体中，感知模块通常位于传感器之后、状态 / 世界模型模块之前：

```text
传感器
  ↓
感知模块
  ↓
状态 / 世界模型模块
  ↓
决策、规划、控制、执行
```

一句话概括：

> 感知模块负责把原始传感器数据转化为智能体可以使用的环境信息。

---

## 2. 模块输入

感知模块可能接收以下输入：

```text
摄像头图像
深度图
RGB-D 数据
LiDAR 点云
IMU 数据
编码器数据
麦克风音频
触觉 / 力传感器数据
GPS 数据
仿真环境观测
```

例子：

```text
摄像头画面
深度相机距离信息
激光雷达点云
无人机局部观测
机器人前方障碍物信息
机械臂末端视觉图像
```

---

## 3. 模块输出

感知模块的输出不是最终动作，而是对环境的结构化理解。

常见输出：

```text
目标物体
障碍物
语义类别
物体位置
深度信息
点云信息
目标检测框
分割结果
人体 / 车辆 / 动物
地面 / 墙体 / 门 / 桌子
视觉特征
感知置信度
```

例子：

```json
{
  "object": "red cup",
  "category": "cup",
  "position_2d": [320, 240],
  "confidence": 0.92
}
```

或者：

```json
{
  "obstacle": true,
  "distance": 1.3,
  "direction": "front"
}
```

---

## 4. 核心知识点与推荐资源

本模块只记录课程级、教材级、系统教程级知识点。
每个知识点至少应该能对应一本书、一门网课或一套系统教程。

---

### 4.1 信号与系统

作用：

> 理解传感器信号、滤波、采样、频域分析，是处理 IMU、音频、控制反馈和传感器数据的基础。

推荐书籍：

* Alan V. Oppenheim, Alan S. Willsky：《Signals and Systems》
* Simon Haykin, Barry Van Veen：《Signals and Systems》

推荐教程 / 网课：

* MIT OCW Signals and Systems
* B站 / 中国大学 MOOC 信号与系统课程
* Coursera / edX Signals and Systems 相关课程

对应项目：

* 传感器数据滤波
* IMU 数据平滑
* 编码器速度信号处理
* 音频指令预处理
* 简单低通 / 高通滤波实验

---

### 4.2 数字图像处理

作用：

> 掌握图像增强、滤波、边缘检测、形态学处理等基础方法，为计算机视觉和机器人视觉打底。

推荐书籍：

* Rafael C. Gonzalez, Richard E. Woods：《Digital Image Processing》
* Rafael C. Gonzalez, Richard E. Woods, Steven L. Eddins：《Digital Image Processing Using MATLAB》

推荐教程 / 网课：

* OpenCV 官方 Tutorials
* 中国大学 MOOC 数字图像处理课程
* B站武汉大学 / 西安电子科技大学数字图像处理课程

对应项目：

* OpenCV 图像读取与显示
* 图像滤波与边缘检测
* 颜色目标检测
* 二值化与形态学处理
* 摄像头画面中的简单障碍物识别

---

### 4.3 计算机视觉

作用：

> 让智能体从图像中识别目标、理解场景、检测障碍物，并提取可用于决策、规划和控制的视觉信息。

计算机视觉在具身智能体中主要用于：

```text
目标识别
目标检测
语义分割
实例分割
目标跟踪
姿态估计
视觉表征学习
机器人视觉定位
障碍物检测
场景理解
```

推荐书籍：

* Richard Szeliski：《Computer Vision: Algorithms and Applications》
* David A. Forsyth, Jean Ponce：《Computer Vision: A Modern Approach》
* Ian Goodfellow, Yoshua Bengio, Aaron Courville：《Deep Learning》
* Aston Zhang 等：《Dive into Deep Learning》

推荐教程 / 网课：

* Stanford CS231n: Deep Learning for Computer Vision
* CMU 16-385 Computer Vision
* Hugging Face Computer Vision Course
* OpenCV 官方 Tutorials
* Ultralytics YOLO 官方文档
* Segment Anything / SAM 官方教程
* DETR / Hugging Face Transformers 视觉模型教程

对应项目：

* 图像分类项目
* YOLO 目标检测
* SAM 图像分割
* DETR 目标检测实验
* 摄像头识别桌面物体
* 机器人前方障碍物检测
* 机械臂抓取前的目标定位
* 无人机识别障碍物和目标区域
* 视觉结果传给状态 / 世界模型模块或决策模块

---

### 4.4 三维视觉

作用：

> 让智能体理解三维空间结构，包括深度、相机几何、三维重建和空间位置估计。

推荐书籍：

* Richard Hartley, Andrew Zisserman：《Multiple View Geometry in Computer Vision》
* Richard Szeliski：《Computer Vision: Algorithms and Applications》

推荐教程 / 网课：

* CMU 16-385 Computer Vision
* CMU 16-720 Computer Vision
* 视觉 SLAM / 多视图几何相关课程
* OpenCV Camera Calibration and 3D Reconstruction Tutorials

对应项目：

* 相机标定
* 单目 / 双目深度估计
* RGB-D 相机三维定位
* 从图像估计物体空间位置
* 相机坐标到机器人坐标转换

---

### 4.5 点云处理

作用：

> 处理 LiDAR、RGB-D 相机等产生的三维点云数据，用于障碍物检测、地图构建和三维感知。

推荐书籍：

* Radu Bogdan Rusu：《Semantic 3D Object Maps for Everyday Manipulation in Human Living Environments》
* Markus Himmelsbach：《Fast Segmentation of 3D Point Clouds for Ground Vehicles》
* 《3D Point Cloud Processing》相关教材或讲义

推荐教程 / 网课：

* Open3D 官方文档
* PCL 官方 Tutorials
* Open3D-ML 官方教程
* LiDAR 感知相关开源教程

对应项目：

* 点云读取与可视化
* 点云滤波
* 平面分割
* 障碍物聚类
* LiDAR 前方障碍物检测
* RGB-D 点云生成

---

### 4.6 传感器技术

作用：

> 理解机器人常用传感器的原理、数据形式、误差特性和使用方式。

推荐书籍：

* Ronald K. Jurgen：《Sensors and Transducers》
* Jacob Fraden：《Handbook of Modern Sensors》
* John Vetelino, Aravind Reghu：《Introduction to Sensors》

推荐教程 / 网课：

* Arduino / STM32 传感器教程
* ROS 2 传感器驱动教程
* Intel RealSense 官方文档
* Livox / Velodyne / RPLIDAR 官方文档
* IMU / LiDAR / RGB-D 相机使用教程

对应项目：

* 摄像头数据读取
* IMU 姿态数据读取
* 超声波测距
* 红外避障
* LiDAR 扫描数据读取
* RGB-D 深度图读取
* 传感器数据传给状态模块

---

### 4.7 多模态感知

作用：

> 将图像、语言、深度、点云、触觉等多种信息融合起来，让智能体更完整地理解环境。

推荐书籍：

* Paul Pu Liang 等：《Multimodal Machine Learning》
* Tadas Baltrušaitis 等：《Multimodal Machine Learning: A Survey and Taxonomy》
* 《Multimodal Deep Learning》相关教材或讲义

推荐教程 / 网课：

* CMU 11-777 Multimodal Machine Learning
* Hugging Face 多模态模型教程
* CLIP / LLaVA / VLM 开源教程
* Vision-Language Model 相关课程

对应项目：

* 图像 + 语言定位目标
* 根据摄像头画面回答环境问题
* 视觉检测结果结合语言任务
* RGB-D + 语义识别
* 为 VLA 模型做前置感知实验

---

## 5. 项目验证

### 5.1 入门项目：摄像头颜色目标检测

目标：

```text
使用摄像头识别指定颜色物体。
```

示例：

```text
输入：摄像头画面
输出：红色物体的位置
```

验证能力：

```text
能读取摄像头
能进行基础图像处理
能输出简单目标位置
```

---

### 5.2 入门项目：OpenCV 障碍物检测

目标：

```text
使用 OpenCV 从图像中检测简单障碍物。
```

功能：

```text
图像读取
图像滤波
边缘检测
轮廓提取
障碍物位置输出
```

验证能力：

```text
能处理图像
能从视觉中提取环境信息
能把结果传给状态 / 决策模块
```

---

### 5.3 进阶项目：YOLO 目标检测

目标：

```text
使用 YOLO 检测机器人视野中的目标物体。
```

示例：

```text
检测桌子、杯子、人、障碍物
输出类别、检测框和置信度
```

验证能力：

```text
能使用深度视觉模型
能识别多个目标
能输出结构化感知结果
```

---

### 5.4 进阶项目：RGB-D 物体三维定位

目标：

```text
使用 RGB-D 相机估计目标物体的三维位置。
```

功能：

```text
读取 RGB 图像
读取深度图
检测目标物体
计算目标物体的三维坐标
```

验证能力：

```text
能把二维视觉结果扩展到三维空间
能为机械臂抓取或移动机器人导航提供目标位置
```

---

### 5.5 高级项目：点云障碍物检测

目标：

```text
使用 LiDAR 或 RGB-D 点云检测环境中的障碍物。
```

功能：

```text
读取点云
滤波
地面分割
障碍物聚类
输出障碍物位置
```

验证能力：

```text
能处理三维点云
能为 SLAM / 导航 / 避障提供环境信息
```

---

### 5.6 高级项目：视觉感知接入机器人系统

目标：

```text
把感知模块输出接入状态 / 世界模型模块或决策模块。
```

示例：

```text
摄像头检测到红色杯子
↓
状态模块记录杯子位置
↓
决策模块判断是否靠近或抓取
```

验证能力：

```text
感知结果不只是显示在屏幕上，而是能被机器人系统使用。
```

---

## 6. 学习状态记录

| 知识点    | 当前状态 |
| ------ | ---- |
| 信号与系统  | 未开始  |
| 数字图像处理 | 入门   |
| 计算机视觉  | 未开始  |
| 深度视觉感知 | 未开始  |
| 三维视觉   | 未开始  |
| 点云处理   | 未开始  |
| 传感器技术  | 了解   |
| 多模态感知  | 了解   |

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

感知模块最终要实现：

```text
智能体能够从摄像头、深度相机、LiDAR、IMU、编码器等传感器中获取信息；
能够识别目标物体、障碍物和环境结构；
能够输出结构化感知结果；
能够将感知结果传给状态 / 世界模型模块、决策模块和规划模块。
```

最终效果：

> 机器人不只是接收原始传感器数据，而是能从数据中提取可用于行动的环境信息。

