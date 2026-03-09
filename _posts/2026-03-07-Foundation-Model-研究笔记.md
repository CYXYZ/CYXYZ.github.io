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

- 研究现状
  - 大致分为两类方法
    - 前瞻性矫正方法：在预防数据采集期间出现伪影。 要在扫描硬件上进行操作，困难而且增加萨扫描时间。
    - 回顾性矫正方法：在数据采集获取后使用`导航器`，`追踪器`，或者`迭代算法` 来移除或者减少伪影。 （可被学术界研究的方法）

### 回顾性矫正方法

- 传统方法
  - 迭代相机相位矫正，自动聚焦，并形成像重建...... 计算高昂且需要辅助数据。比如原始频率域(k-space)数据

- 深度学习方法
  - 去缠绕的五监督循环一致对抗网络(DUNCAN)

### 部分 1

### 部分 2

### 部分 3

## 总结

## 参考资源
