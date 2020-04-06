---
title: AEM系统概述
description: AEM系统概述
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# AEM系统概述 {#aem-system}

本页将AEM描述为云服务，该服务通过体系结构提供新功能，该体系结构较之先前的AEM版本具有显着增强。 升级到此新架构需要付出大量努力。

## 描述 {#background}

ACRA元模式用于确定与作为云服务升级到AEM相关的几个问题。 它通过模式的referring和“referencedBy”值及其上下文对象的 *组合* ，支持几种类型的建 *议信息* 。 上 *下文对象* 中的类型 ** 值确定已检测到的特定问题。

ACRA模式中包括的准备问题预计导致建议的实例相对较少。 AEM作为云服务存在其他与准备就绪性问题，这些问题可能有许多实例需要注意，并且这些实例会得到它们自己的模式代码。 （请参阅用户界面和用户。）

## 图案数据 {#pattern-data}

模式的JSON表示中包含以下对象：

* **item.message**:就绪问题类型。 （请参阅下文。）
* **数据**:包含与类型对应的数据的JSON对象。

### 可能的影响和风险 {#possible-implications}

TBD

### 可能的解决方案 {#possible-solutions}

TBD
