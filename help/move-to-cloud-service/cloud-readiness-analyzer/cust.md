---
title: 检测到自定义
description: 检测到自定义
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 3%

---


# 检测到自定义 {#cust-pattern}

本页介绍“Customization Detected”模式代码。

## 背景 {#background}

此模式代码用于标识已对AEM实例进行的自定义。 由于AEM的自定义很常见，因此此模式不一定表示有问题。 它标识自定义记录，以便根据对升级计划的影响对其进行评估。

检测到的自定义包括：

* 客户代码（包）和配置
* 第三方包
* 与第三方服务集成
* 非标准Oak索引

## 图案数据 {#pattern-data}

模式的JSON表示中包含以下对象：

* **item.message**: 指模式的信息。
* **item.context**: 请参阅有关概述信息的其他信息：
   * *类型*: customization.detected.
   * *数据*: 包含描述自定义的数据的JSON对象

### 可能的影响和风险 {#possible-implications}

不适用.

### 可能的解决方案  {#possible-solutions}

不适用.
