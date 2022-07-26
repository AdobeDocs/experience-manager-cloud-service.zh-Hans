---
title: 内容片段 — 配置浏览器
description: 了解如何在配置浏览器中启用某些内容片段功能，以便利用AEM功能强大的无头交付功能。
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 23%

---

# 内容片段 — 配置浏览器{#content-fragments-configuration-browser}

了解如何在配置浏览器中启用某些内容片段功能，以便利用AEM功能强大的无头交付功能。

## 为您的实例启用内容片段功能 {#enable-content-fragment-functionality-instance}

在使用内容片段之前，您需要使用 **配置浏览器** 启用：

* **内容片段模型**  — 必填
* **GraphQL持久查询**  — 可选

>[!CAUTION]
>
>如果未启用 **内容片段模型**:
>
>* the **创建** 选项将不可用于创建新模型。
>* 你将无法 [选择站点配置以创建相关的端点](/help/headless/graphql-api/graphql-endpoint.md).


要启用内容片段功能，您需要：

* 通过配置浏览器启用内容片段功能的使用
* 将配置应用到Assets文件夹

### 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用某些内容片段功能](#creating-a-content-fragment-model) you **必须** 首先，通过 **配置浏览器**:

>[!NOTE]
>
>有关更多详细信息，另请参阅 [配置浏览器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子配置](/help/implementing/developing/introduction/configurations.md#configuration-resolution) 完全支持与内容片段、内容片段模型和GraphQL查询一起使用（嵌套在另一个配置中的配置）。
>
>请注意：
>
>
>* 在子配置中创建模型后，无法将模型移动或复制到另一个子配置。
>
>* GraphQL端点将（仍然）基于父（根）配置。
>
>* 将（仍）保存与父（根）配置相关的持久化查询。



1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用 **创建** 要打开对话框，您需要：

   1. 指定 **标题**.
   1. **名称**&#x200B;将成为存储库中的节点名称。
      * 它会根据标题自动生成，并根据 [AEM 命名约定](/help/implementing/developing/introduction/naming-conventions.md)进行调整。
      * 您可以根据需要进行调整。
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cfm-conf-01.png)


1. 选择 **创建** 以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到您的Assets文件夹 {#apply-the-configuration-to-your-assets-folder}

配置 **全球** ，则会应用于任何资产文件夹。

要将其他配置（即不包括全局配置）与类似的 Assets 文件夹一起使用，您必须定义连接。这是通过在相应文件夹的“ **文件夹属性** ”的“云服务 **”选项卡中选****** 择相应的配置来完成的。

![应用配置](assets/cfm-conf-02.png)
