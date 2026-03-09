---
layout:     post
title:      BME-X 研究笔记
subtitle:   
date:       2026-03-07
author:     CYXYZ
header-img: img/foundation-model.png
catalog: true
category:   Foundation Model
tags:
    - Foundation Model
---

# A foundation model for enhancing magnetic resonance images and downstream segmentation, registration and diagnostic tasks

## 论文PDF

<iframe src="{{ site.baseurl }}/pdf/Sun 等 - 2024 - A foundation model for enhancing magnetic resonance images and downstream segmentation, registration.pdf" width="100%" height="600" frameborder="0"></iframe>

## 简介

报告了一个用于MRI图像的运动校正、分辨率增强、降噪和和谐优化的基础模型。模型可以将 3-T 扫描生成 7-T 形状的图像，并协调来自不同扫描仪的图像。通过模型生成的图像可以用于提高组织分割，配准，诊断和其他下游任务的性能。

## 研究目标

- 核心问题
  - `MRI` 数据在成像过程中会因为运动，心跳，呼吸或眨眼导致**严重模糊和运动伪影**。
  - 在 2-4 岁的小孩儿中收集 **高质量的MRI** 具有挑战性，因为他们非常活跃。
  - **多中心数据异质性问题**。因为设备制造商，型号和成像参数差异导致的 数据难以比较，合并和用于统一的模型训练或临床研究。

### 对于 `运动伪影` 问题：

- 研究现状
  - 大致分为两类方法
    - 前瞻性矫正方法：在预防数据采集期间出现伪影。 要在扫描硬件上进行操作，困难而且增加萨扫描时间。
    - 回顾性矫正方法：在数据采集获取后使用`导航器`，`追踪器`，或者`迭代算法` 来移除或者减少伪影。 （可被学术界研究的方法）

#### 回顾性矫正方法

- 传统方法
  - 迭代相机相位矫正，自动聚焦，并形成像重建...... 计算高昂且需要辅助数据。比如原始频率域(k-space)数据

- 深度学习方法
  - 多尺度全卷及神经网络，去缠绕的无监督循环一致对抗网络(DUNCAN)。
    - 问题：会产生残留伪影和解剖结构不正确的图像

### 对于 `严重模糊` 问题：

- 研究现状
  - 成像硬件，信噪比，时间限制和受试者舒适度限制导致的低分辨率  --> 超分辨技术
    - 非本地 MRI 上采样方法 (NLUP)
    - (SynthSR)
  
  - 热噪声，随机变化，生理过程引起的成像退化 --> 降噪声


**目前的方法将上述的运动矫正，超分辨和去噪声视为独立的任务，导致累积误差。**

针对上述问题，提出 `BME-X`，一个 **脑MRI** 增强基础模型.
- 基本假设
  - 提高图像质量会产生更清晰，更锐利的图像外观。即图像质量越高，同一种组织的像素强度越接近一个固定值。

换句话说：如果可以把每个像素属于什么组织准确分类，那么高质量图像就可以根据这些分类结果反推出来。所以重建任务被简化为一个组织分类任务。

所以，`BME-X` 模型由组织分类网络和组织感知增强网络组成。
- 组织分类网络用于预测组织标签；
- 组织感知增强网络利用这些组织标签生成高质量的图像。

## 研究数据和结果

这里只关注研究数据量和使用的标准。

对 `2448 张` 合成的退化图像和来自 `19 个`公开数据集的 `10963` 张活体图像进行验证，包含西门子，通用电子和菲利普扫描仪，涵盖了从胎儿到老年人的整个生命周期。

### 核心实验
- 来自 6 个数据集(1-2岁儿童)的`2088` 个合成退化图像上和来自 19 个数据集的 `10963` 张真实的体内扫描图像上验证模型优势。
- 消融实验
- 处理不同程度的 运动伪影，下采样，高斯噪声，Rician噪声，平滑模糊，确认模型在各种退化情况下都能稳定工作。
- 分析是否改变组织结构和产生了系统性偏差
- 从 3T 图像中生成 7T-like 图像
- 处理病变的 MRI
- 处理多中心数据的跨扫描仪差异问题
- 下游任务评估

### 评估指标
对于**合成数据**，使用 **多分辨率非局部均值滤波** 得到可靠的无伪影图像。
分别使用下面的六种图像质量指标：
- **MSE**  逐像素差异（越低越好）
- **PSNR**   峰值信噪比，由 MSE 推导（越高越好）
- **SSIM**   结构相似度 亮度、对比度、结构相似度（越高越好）
- **MS-SSIM**   多尺度版本的 SSIM（越高越好）
- **UQI**   通用质量指数 从相关性、亮度、对比度三个方面建模的失真（越高越好）
- **VIF**  方差膨胀因子 衡量参考图像与退化图像共享的信息量（越高越好）

对于**活体数据**，没有无缺陷的参考标准，采用组织对比模糊分数(TCT):
\begin{equation}
\text{TCT} = \frac{|\mu_{\text{wm}} - \mu_{\text{gm}}|}{\sqrt{\sigma_{\text{wm}}^2 + \sigma_{\text{gm}}^2}},
\end{equation}
其中，$(\mu_{\text{wm}}, \sigma_{\text{wm}}^2)$ 和 $(\mu_{\text{gm}}, \sigma_{\text{gm}}^2)$ 分别是白质（White Matter, WM）和灰质（Grey Matter, GM）亮度的均值与方差。文章中使用 `iBEAT V2.0` 工具 来提取白质和灰质区域进行计算。


对于对比试验，还计算了部分的 p-value 以衡量是否有统计学意义。

## 研究方法
通常情况下，如果低质量图像$I$的强度范围是$\[0,m\]$，高质量图像$I_0$的强度范围是$\[0,n\]$，因为高质量图像的强度值和低质量图像中强度值是任意互相映射的，所以每个体素的计算复杂度为 $O(m\times n)$。但转化为一个分类问题后，这个问题被拆解为 原始图像 $I$ --> 组织分类图 $L_c$ + 组织分类图 $L_c$ --> 增强图像 $I_0$，所以每个体素的计算复杂度变为 $O(m+n)$。
<p style="color:gray; font-size:16px;">
Tip: 因为之前每个像素值需要在 $m*n$ 的可能性中找一个映射；而转换之后只需要完成一个 $m*1$ 和 $1*n$ 的任务即可。
</p>

### 分类任务模型
输入 低质量图像 --> 选择 **DU-Net** 作为主干分类模型 + 交叉熵损失函数 --> 输出 组织分类地图
输入 组织分类概率地图 + 低质量图像 -->  选择 **DU-Net** 作为增强模型的骨干 + 与高质量图像的 MSE 损失函数 --> 输出高质量图像

### 补充
#### 训练数据
为了找到 `成对的高低质量 MRI 图像`，通过在高质量MRI数据上施加多样性的伪影来得到对应的低质量MRI图像。
- 采用参考文献 60  中的 `view2Dmotion 软件模拟图像运动` 和 图像模拟软件 79 中的 `Frnet 添加模糊噪声` 来生成带伪影的图片。
- 使用 `Caffe` 作为训练框架
- 使用 `iBEAT V2.0` 工具 生成组织分类标签
- 数据来源 
  - 公开数据集`BCP (Baby Connectome Project)`：用于 0-6 岁婴幼儿模型的训练 。数据托管在 NDA（National Database for Autism Research），链接 为 https://nda.nih.gov/edit_collection.html?id=2848 。
  - 团队采集数据： 用于胎儿阶段（21-36 周）训练的 52 名参与者数据属于研究团队自有的内部数据 。
- 训练了针对不同年龄段的 增强任务模型 包括：0个月，3个月，6个月，9个月，12个月，18个月和24个月。
- 对于每个图像随即抽取 2000 个补丁进行训练

#### 测试数据
通过 19 个公开数据集验证了模型的泛化能力：

1. 
**dHCP** (Developing Human Connectome Project): 专注于新生儿阶段 。
2. 
**NDAR** (National Database for Autism Research): 包含婴幼儿及发育研究数据 。
3. 
**BCP** (Baby Connectome Project): 核心数据集，用于 0-6 岁婴幼儿训练与测试 。
4. 
**SALD** (Southwest University Adult Lifespan Dataset): 西南大学收集的成人寿命数据集 。
5. 
**CCNP** (Chinese Color Nest Project): 专注于中国人群的大脑发育研究 。
6. 
**DLBS** (Dallas Lifespan Brain Study): 达拉斯寿命大脑研究 。
7. 
**IXI** (Information eXtraction from Images): 包含来自伦敦三家医院的成人数据 。
8. 
**Chinese Adult Brain**: 中国成人脑图谱数据集 。
9. 
**ABIDE** (Autism Brain Imaging Data Exchange): 自闭症脑成像数据交换 。
10. 
**ABVIB** (Aging Brain: Vasculature, Ischemia, and Behavior): 衰老大脑的血管、缺血与行为研究 。
11. 
**ADNI** (Alzheimer's Disease Neuroimaging Initiative): 阿尔茨海默症研究，用于测试模型在病理性大脑上的表现 。
12. 
**AIBL** (Australian Imaging, Biomarkers and Lifestyle): 澳大利亚老龄化研究数据集 。
13. 
**HBN** (Healthy Brain Network): 健康大脑网络，涵盖青少年发育数据 。
14. 
**HCP** (Human Connectome Project): 人类连接组计划，高质量成人脑成像标杆 。
15. 
**ICBM** (International Consortium for Brain Mapping): 国际脑图谱联合会数据集 。
16. 
**OASIS3** (Open Access Series of Imaging Studies 3): 纵向神经成像数据集，涵盖正常老化与 AD 。
17. 
**SLIM** (Southwest University Longitudinal Imaging Multimodal): 西南大学纵向多模态成像库 。
18. 
**MR-ART** (Movement-Related Artefacts): 专门包含“运动伪影”与“对照组”的成人数据集，用于验证真实伪影去除效果 。
19. 
**T2w foetal images** (In-house collection): 内部收集的胎儿 T2 加权图像，涉及 142 名参与者 。

上述的数据集中共使用2088张合成数据和10963张活体数据：
- 合成数据：来自BCP, NDAR, SALD, CCNP, DLBS and IXI 数据集，都通过相同量的周期运动来合成严重损坏的图像。然后反向对比评估。
- 活体数据：每一位参与者在保持静止，轻微头部运动和更为过度的头部运动三种条件下进行扫描。**但静止图像并不能作为增强结果的基准数据，因为无法建立运动图像和受损图像之间的体素对应关系**
