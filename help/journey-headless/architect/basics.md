---
title: 学习内容建模基础知识
description: 学习使用内容片段为 Headless CMS 的内容建模的基础知识。
exl-id: dc460490-dfc8-4a46-a468-3d03e593447d
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 100%

---

# 学习使用 AEM 对 Headless 进行内容建模的基础知识 {#content-modeling-headless-basics}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容架构师历程](overview.md)的开头，[简介](introduction.md)涵盖了与针对 Headless 进行内容建模相关的基本概念和术语。

本文基于这些内容编写，以便您了解如何对 AEM Headless 项目进行内容建模。

## 目标 {#objective}

* **受众**：初学者
* **目标**：介绍 Headless CMS 的内容建模概念。

## 使用内容片段模型进行内容建模 {#architect-content-fragment-models}

内容（数据）建模是一系列成熟的技术，在开发关系数据库时通常会使用这些技术，那么内容建模对 AEM Headless 意味着什么呢？

### 为什么？ {#why}

为了确保您的应用程序能够一致而高效地从 AEM 请求和接收所需内容，必须设置这些内容的结构。

这意味着您的应用程序会预先知道响应的形式，从而了解如何处理它。这比接收自由格式的内容要简单得多，必须对自由格式的内容进行分析以确定它包含什么以及如何使用它。

### 方法简介 {#how}

AEM 使用内容片段提供以 Headless 方式将内容交付到应用程序所需的结构。

内容模型的结构将：

* 由内容片段模型的定义识别，
* 用作用于内容生成的内容片段的基础。

>[!NOTE]
>
>内容片段模型还用作 AEM GraphQL 架构的基础，用于检索您的内容 - 开发人员历程中提供了更多相关信息。

使用 AEM GraphQL API 发出对您的内容的请求，这是标准 GraphQL API 的自定义实施。AEM GraphQL API 允许应用程序对内容片段执行（复杂）查询，每个查询都根据特定的模型类型执行。

然后，您的应用程序可以使用返回的内容。

## 使用内容片段模型创建结构 {#create-structure-content-fragment-models}

内容片段模型提供了多种机制，可让您定义内容的结构。

内容片段模型描述了一个实体。

>[!NOTE]
>必须在配置浏览器中启用内容片段功能，才能创建新模型。

>[!TIP]
>
>应对模型命名，以便内容作者在创建内容片段时知道选择哪个模型。

在模型中：

1. **数据类型**可让您定义单个属性。
例如，以**文本**&#x200B;形式定义包含教师姓名的字段，并以&#x200B;**数字**&#x200B;形式定义其服务年数。
1. 数据类型&#x200B;**内容引用**&#x200B;和&#x200B;**片段引用**&#x200B;可让您在 AEM 中创建与其他内容的关系。
1. **片段引用**&#x200B;数据类型可让您通过嵌套内容片段（根据模型类型）来实施结构的多个层次。这对于您的内容建模是至关重要的。

例如：

![使用内容片段进行内容建模](assets/headless-modeling-01.png "使用内容片段进行内容建模")

## 数据类型 {#data-types}

AEM 提供了以下数据类型以供您用来进行内容建模：

* 单行文本
* 多行文本
* 数字
* 布尔值
* 日期和时间
* 枚举
* 标记
* 内容引用
* 片段引用
* JSON 对象

>[!NOTE]
>
>“内容片段模型 - 数据类型”下提供了更多详细信息。

## 引用和嵌套内容 {#references-nested-content}

两种数据类型都提供了对特定片段之外的内容的引用：

* **内容引用**
这提供了对任意类型的其他内容的简单引用。
例如，您可以在指定位置引用图像。

* **片段引用**
这会提供对其他内容片段的引用。
这种类型的引用用于创建嵌套内容，引入对内容进行建模所需的关系。
数据类型可配置为允许片段作者执行以下操作：
   * 直接编辑引用的片段。
   * 根据相应的模型创建新内容片段

>[!NOTE]
>
>您还可以通过使用文本块中的链接来创建临时引用。

## 结构层次（嵌套片段） {#levels-of-structure-nested-fragments}

对于内容建模，**片段引用**&#x200B;数据类型可让您创建结构的多个层次和关系。

借助此引用，您可以&#x200B;*连接*&#x200B;各种内容片段模型来表示相互关系。这可让 Headless 应用程序遵循连接并在必要时访问内容。

>[!NOTE]
>
>应谨慎使用此引用，最佳实践可以定义为&#x200B;*进行所需数量的嵌套，越少越好*。

片段引用是这样做的 - 它们允许您引用其他片段。

例如，您可能定义了以下内容片段模型：

* 城市
* 公司
* 人员
* 奖励

似乎很简单，一家公司肯定会有一个 CEO 和众多员工....他们每个人都被定义为一个人员。

一个人员可以获得一个（或两个）奖励。

* 我的公司 – 公司
   * CEO – 人员
   * 员工 – 人员
      * 个人奖励 – 奖励

这只适用于初学者。根据复杂性，奖励可以是特定于公司的，或者公司可以在特定城市设立主要办事处。

可以使用片段引用来表示这些相互关系，因为您（架构师）、您的内容作者和 Headless 应用程序都已理解它们。

## 后续内容 {#whats-next}

现在您已了解基础知识，下一步是[了解如何在 AEM 中创建内容片段模型](model-structure.md)。这将介绍和讨论可用的各种引用，以及如何使用片段引用创建结构层次 - 针对 Headless 的建模的关键部分。

## 其他资源 {#additional-resources}

* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

   * [内容片段模型 – 数据类型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本处理](/help/sites-cloud/authoring/getting-started/basic-handling.md) – 此页面主要基于&#x200B;**站点**&#x200B;控制台，但许多/大多数功能也用于在 **Assets** 控制台下创作&#x200B;**内容片段**。

* [使用内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
