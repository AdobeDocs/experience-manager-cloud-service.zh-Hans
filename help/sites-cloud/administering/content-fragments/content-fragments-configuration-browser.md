---
title: 内容片段 – 配置浏览器
description: 了解如何在配置浏览器中启用内容片段和GraphQL功能，以使用AEM Headless投放功能。
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 1fc57dacbf811070664d5f5aaa591dd705516fa8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 34%

---

# 内容片段 – 配置浏览器{#content-fragments-configuration-browser}

了解如何在配置浏览器中启用特定的内容片段功能。

## 为您的实例启用内容片段功能 {#enable-content-fragment-functionality-instance}

在使用内容片段之前，您必须使用 **配置浏览器** 要启用，请执行以下操作：

* **内容片段模型** – 强制
* **GraphQL 持久查询** – 可选

>[!CAUTION]
>
>如果未启用&#x200B;**内容片段模型**：
>
>* 此 **创建** 选项不可用于创建模型。
>* 您不能 [选择Sites配置以创建相关端点](/help/headless/graphql-api/graphql-endpoint.md).

要启用内容片段功能，您必须执行以下操作：

* 通过配置浏览器启用内容片段功能
* 将配置应用到 Assets 文件夹

### 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

使用特定 [内容片段功能](#creating-a-content-fragment-model)，您 **必须** 首先通过 **配置浏览器**：

>[!NOTE]
>
>有关更多详细信息，请参阅 [配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子配置](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （嵌套在另一个配置中的配置）完全支持与内容片段、内容片段模型和GraphQL查询一起使用。
>
>请注意：
>
>
>* 在子配置中创建模型后，无法将模型移动或复制到另一个子配置。
>
>* GraphQL端点（仍然）基于父（根）配置。
>
>* 与父（根）配置相关的持久查询（仍）已保存。


1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**“创建”**&#x200B;来打开对话框，您需要：

   1. 指定&#x200B;**标题**。
   1. 此 **名称** 将成为存储库中的节点名称。
      * 它根据标题自动生成，并根据以下内容进行调整 [AEM命名约定。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有必要，您可以对其进行调整。
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cfm-conf-01.png)

1. 选择&#x200B;**“创建”**&#x200B;以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到文件夹 {#apply-the-configuration-to-your-folder}

当配置 **全局** 已启用内容片段功能，它适用于任何资产文件夹 — 可通过访问 **资产** 控制台。

要将其他配置（即不包括全局配置）与类似的Assets文件夹一起使用，您必须定义连接。 此连接可通过选择适当的 **配置** 在 **Cloud Services** 的选项卡 **文件夹属性** 文件夹中的。

![应用配置](assets/cfm-conf-02.png)
