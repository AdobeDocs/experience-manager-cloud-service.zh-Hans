---
title: 了解如何在 AEM 中创建内容片段模型
description: 了解使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 6306ad88b889197aff377dc0a72ea232cd76ff9c
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 76%

---

# 了解如何在 AEM 中创建内容片段模型 {#architect-headless-content-fragment-models}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[使用 AEM 对 Headless 进行内容建模的基础知识](basics.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

本文基于这些原则之上，以便您了解如何为AEM Headless项目创建自己的内容片段模型。

## 目标 {#objective}

* **受众**：初学者
* **目标**：使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools > General > Configuration Browser. You can either select to configure the global entry, or create a configuration. For example:

![Define configuration](/help/sites-cloud/administering/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## 创建内容片段模型 {#creating-content-fragment-models}

然后，可以创建内容片段模型并定义结构。

1. 在内容片段控制台中，为内容片段模型选择面板。

1. 导航到适合您的配置或子配置的文件夹。

1. 使用&#x200B;**创建**&#x200B;打开&#x200B;**新内容片段模型**&#x200B;对话框。

   ![标题和描述](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. 完成详细信息

1. 使用&#x200B;**创建**&#x200B;保存空模型，或使用&#x200B;**创建并打开**。

<!--
Then the Content Fragments Models can be created and the structure defined. This can be done under **Tools** > **General** > **Content Fragment Models**. 

![Content Fragment Models in Tools](assets/cfm-tools.png)

After selecting this you navigate to the location for your model and select **Create**. Here you can enter various key details.

The option **Enable model** is activated by default. This means that your model is available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![Create Content Fragment Model](/help/sites-cloud/administering/content-fragments/assets/cfm-models-02.png)

Confirm with **Create** and you can then **Open** your model to start defining the structure.
-->

## 定义内容片段模型 {#defining-content-fragment-models}

当您首次打开一个新模型时，您将看到左侧有一个大的空白区域，右侧有一个较长的&#x200B;**数据类型**&#x200B;列表：

![空白模型](/help/sites-cloud/administering/content-fragments/assets/cfm-models-03.png)

那么——该如何操作？

您可以将&#x200B;**数据类型**&#x200B;的实例拖到左侧空白区域，您已定义模型！

![定义字段](/help/sites-cloud/administering/content-fragments/assets/cfm-models-04.png)

在添加数据类型后，您需要为该字段定义&#x200B;**属性。**&#x200B;这些属性取决于所使用的类型。 例如：

![数据属性](/help/sites-cloud/administering/content-fragments/assets/cfm-models-05.png)

可以添加所需数量的字段。例如：

![内容片段模型](/help/sites-cloud/administering/content-fragments/assets/cfm-models-07.png)

### 您的内容作者 {#your-content-authors}

您的内容作者看不到您用于创建模型的实际数据类型和属性。这意味着您可能需要提供有关他们如何填写特定字段的帮助和信息。对于基本信息，您可以使用字段标签和默认值，但在更复杂的情况下，可能需要考虑项目特定的文档。

>[!NOTE]
>
>请参阅“其他资源——内容片段模型”。

## 管理内容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理内容片段模型涉及：

* 启用（或禁用）内容片段模型——这使作者在创建内容片段时能够使用它们。
* 删除 — 始终需要删除，但您需要了解如何删除已用于内容片段的模型；尤其是已发布的片段。

## 发布 {#publishing}

<!-- needs more details -->

在发布任何相关内容片段时/之前，需要发布内容片段模型。

>[!NOTE]
>
>如果作者尝试发布的内容片段尚未发布模型，则会显示一个选择列表来指示该行为，并且模型会与片段一起发布。

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
