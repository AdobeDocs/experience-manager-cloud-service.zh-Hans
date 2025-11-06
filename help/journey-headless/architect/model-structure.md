---
title: 了解如何在 AEM 中创建内容片段模型
description: 了解使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 83%

---

# 了解如何在 AEM 中创建内容片段模型 {#architect-headless-content-fragment-models}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[使用 AEM 对 Headless 进行内容建模的基础知识](basics.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

本文基于这些原则编写，以便您了解如何为 AEM Headless 项目创建您自己的内容片段模型。

## 目标 {#objective}

* **受众**：初学者
* **目标**：使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。

## 创建内容片段模型 {#creating-content-fragment-models}

之后，可以创建内容片段模型并定义结构。

1. 在内容片段控制台中，选择内容片段模型面板。

1. 导航到适合您的配置或子配置的文件夹。

1. 使用&#x200B;**创建**，打开&#x200B;**新内容片段模型**&#x200B;对话框。

   ![标题和描述](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. 填写详细信息

1. 使用&#x200B;**创建**&#x200B;保存空模型，或者&#x200B;**创建并打开**。

## 定义内容片段模型 {#defining-content-fragment-models}

首次打开新模型时，您会看到 — 中间有一大块（相当大的）空白，左侧有一长串&#x200B;**数据类型**，右侧有一长串&#x200B;**属性**（开始处是空的，与选定字段的属性相同）：

![空白模型](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-empty-model.png)

那么——该如何操作？

您可以：

* 将数据类型从左侧面板拖到中间面板中字段的所需位置。
* 按数据类型选择+图标以将其添加到字段列表的底部。
* 选择中间面板中的“添加”，然后从结果下拉列表中选择所需的数据类型，以在列表底部添加字段。

您已在定义模型！

在添加数据类型后，您需要为该字段定义&#x200B;**属性。**&#x200B;这些属性都取决于将使用的类型。例如：

![数据属性](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-field-properties.png)

### 您的内容作者 {#your-content-authors}

您的内容作者看不到您用于创建模型的实际数据类型和属性。这意味着您可能需要提供有关他们如何填写特定字段的帮助和信息。对于基本信息，您可以使用字段标签和默认值，但在更复杂的情况下，可能需要考虑项目特定的文档。

>[!NOTE]
>
>请参阅“其他资源——内容片段模型”。

## 管理内容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理内容片段模型涉及：

* 启用（或禁用）内容片段模型——这使作者在创建内容片段时能够使用它们。
* 删除——始终需要执行删除操作，但您需要注意删除已用于内容片段的模型，特别是已发布的片段。

## 发布 {#publishing}

<!-- needs more details -->

在发布任何相关内容片段时/之前，需要发布内容片段模型。

>[!NOTE]
>
>如果作者尝试发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

模型一经发布，就会&#x200B;*锁定*&#x200B;为作者的只读架构。这旨在阻止进行可能导致现有 GraphQL 架构和查询出错的更改，尤其是在发布环境中。它在控制台中由&#x200B;**已锁定**&#x200B;指示。

当模型处于&#x200B;**已锁定**&#x200B;状态（在只读架构中）时，您可以查看模型的内容和结构，但无法直接编辑它们；但您可以从控制台或模型编辑器中管理&#x200B;**已锁定**&#x200B;模型。

## 后续内容 {#whats-next}

现在您已了解基础知识，下一步是开始创建您自己的内容片段模型。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-cloud/authoring/author-publish.md)

* [基本处理](/help/sites-cloud/authoring/basic-handling.md)——此页面主要基于&#x200B;**Sites**&#x200B;控制台，但许多/大多数功能也用于在&#x200B;**常规**&#x200B;控制台下导航到并操作&#x200B;**内容片段模型**。

* [使用内容片段](/help/sites-cloud/administering/content-fragments/overview.md)

   * [内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [定义内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [启用或禁用内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [允许在 Assets 文件夹中使用内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [删除内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [发布内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [取消发布内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [锁定的内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* 快速入门指南

   * [创建内容片段模型 Headless 设置](/help/headless/setup/create-content-model.md)
