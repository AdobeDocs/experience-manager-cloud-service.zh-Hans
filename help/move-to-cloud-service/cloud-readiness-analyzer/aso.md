---
title: AEM系统概述
description: AEM系统概述
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%

---


# AEM系统概述 {#aem-system}

本页介绍Adobe Experience Manager(AEM)系统概述。

## 背景 {#background}

此模式用于标识提供AEM系统概述的一般信息。 信息可包括以下项目：

使用的AEM版本AEM产品（站点、资产、表单等）节点计数（页面、资产等）

## 图案数据 {#pattern-data}

模式的JSON表示中包含以下对象：

* **item.message**: 指模式的信息。
* **item.context**: 请参阅有关概述信息的其他信息：
   * *类型*: 上下文数据的类型，“aem.version”、“aem.product”或“node.count”。
   * *数据*: 包含与类型对应的数据的JSON对象： “version”（字符串）、“product”（字符串）或“count”（整数）。

### 可能的影响和风险 {#possible-implications}

不适用.

### 可能的解决方案  {#possible-solutions}

不适用.
