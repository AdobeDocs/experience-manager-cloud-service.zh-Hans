---
title: AEM系统概述
description: AEM系统概述
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# AEM系统概述 {#aem-system}

本页将AEM描述为一种云服务，它通过一种体系结构提供新功能，该体系结构较早期的AEM版本具有显着增强。 升级到此新架构需要付出大量努力。

## 描述 {#background}

ACRA元模式用于确定与作为云服务升级到AEM相关的几个问题。 它通过模式的引用值和“referencedBy”值及其上下文对 *象的组* 合支持几种类型的建 *议信息* 。 上 *下文对* 象中 *的类型* 值确定已检测到的特定问题。

ACRA模式中包括的准备问题预计只有较少的实例导致建议。 与AEM云服务形式相关的其他就绪性问题可能有许多实例需要关注，并且这些实例会得到自己的模式代码。 （请参阅UUI和UURS。）

## 图案数据 {#pattern-data}

模式的JSON表示中包含以下对象：

* **item.message**: 就绪问题类型。 （请参阅下文。）
* **数据**: 包含与类型对应的数据的JSON对象。

### 可能的影响和风险 {#possible-implications}

TBD

### 可能的解决方案  {#possible-solutions}

TBD
