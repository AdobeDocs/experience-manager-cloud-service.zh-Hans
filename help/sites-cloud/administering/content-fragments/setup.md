---
title: 内容片段 — 设置
description: 了解如何启用内容片段和GraphQL功能以使用AEM Headless投放功能。
feature: Content Fragments
role: Developer, Architect
source-git-commit: 676173813b6ea4defeafe25c95be9668d32aac38
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 37%

---


# 内容片段 — 设置 {#content-fragments-setup}

利用Adobe Experience Manager (AEM) as a Cloud Service中的内容片段，您可以准备内容以用于多个位置和多个渠道。 这非常适用于headless投放和页面创作。

要为内容片段功能启用实例，您需要启用：

* **内容片段模型** – 强制

  >[!CAUTION]
  >
  >如果未启用&#x200B;**内容片段模型**：
  >
  >* 该 **创建** 选项将不可用于创建模型。
  >* 你将无法[选择 Sites 配置来创建相关的端点](/help/headless/graphql-api/graphql-endpoint.md)。

* **GraphQL 持久查询** – 可选

设置实例已完成：

* 按 [在配置浏览器中启用功能](#enable-content-fragment-functionality-configuration-browser)
* 则 [将配置应用于您的单个资源文件夹](#apply-the-configuration-to-your-folder)

## 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-configuration-browser}

要使用内容片段功能、内容片段模型和GraphQL持久查询，您可以 **必须** 首先通过 **配置浏览器**：

>[!NOTE]
>
>有关更多详细信息，请参阅 [配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子配置](/help/implementing/developing/introduction/configurations.md#configuration-resolution)（嵌套在另一个配置中的配置）完全支持与内容片段、内容片段模型和 GraphQL 查询一起使用。
>
>请注意：
>
>* 在子配置中创建模型后，无法将模型移动或复制到另一个子配置。
>
>* GraphQL 端点将（仍然）基于父（根）配置。
>
>* 将（仍）保存与父（根）配置相关的持久查询。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**“创建”**&#x200B;来打开对话框，您需要：

   1. 指定&#x200B;**标题**。
   1. 创建后， **名称** 将成为存储库中的节点名称。
您可以输入名称。 如果将该字段留空，则它会根据标题自动生成，然后根据进行调整 [AEM命名约定](/help/implementing/developing/introduction/naming-conventions.md)；您可以根据需要调整结果。
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cf-setup-create-conf.png)

1. 选择&#x200B;**“创建”**&#x200B;以保存定义。

## 将配置应用到文件夹 {#apply-the-configuration-to-your-folder}

配置时 **全局** 启用内容片段功能后，该功能随后会应用到任何资产文件夹 — 可通过访问 **资产** 控制台。

要将其他配置（因此不包括全局配置）与类似的Assets文件夹一起使用，您必须定义连接。 选择适当的 **配置** 在 **Cloud Service** 选项卡 **文件夹属性** 文件夹中的URL。

![应用配置](assets/cf-setup-apply-conf.png)
