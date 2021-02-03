---
title: 创建内容片段无头快速开始指南
description: 内容片段允许您设计、创建、管理和使用AEM可以无头地交付的与页面无关的内容。
translation-type: tm+mt
source-git-commit: fa2fee3139acd60ea96222752785cf397978a2bc
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# 创建内容片段无头快速开始指南{#creating-content-fragments}

内容片段允许您设计、创建、管理和使用AEM可以无头地交付的与页面无关的内容。

## 什么是内容片段？{#what-are-content-fragments}

[现在，您已创建了一个资产](create-assets-folder.md) 文件夹，您可以在其中存储内容片段，现在您可以创建片段！

内容片段允许您设计、创建、管理和发布与页面无关的内容。 它们允许您准备内容，准备好在多个位置和多个渠道中使用。

内容片段包含结构化内容，可以以JSON格式提供。

## 如何创建内容片段{#how-to-create-a-content-fragment}

内容作者将创建任意数量的内容片段来代表他们创建的内容。 这将是他们在AEM的主要任务。 为了本入门指南的目的，我们只需创建一个。

1. 以Cloud Service身份登录AEM，并从主菜单中选择&#x200B;**导航->资产**。
1. 点按或单击您之前创建的[文件夹。](create-assets-folder.md)
1. 点按或单击&#x200B;**创建->内容片段**。
1. 内容片段的创建通过两个步骤呈现为向导。 首先选择要用于创建内容片段的模型，然后点按或单击&#x200B;**下一步**。
   * 可用的模型取决于您为资产文件夹](create-assets-folder.md)定义的&#x200B;[**云配置**，您在其中创建内容片段。
   * 如果收到消息`We could not find any models`，请检查资产文件夹的配置。

   ![选择内容片段模型](../assets/content-fragment-model-select.png)
1. 根据需要提供&#x200B;**标题**、**说明**&#x200B;和&#x200B;**标记**，然后点按或单击&#x200B;**创建**。

   ![创建内容片段](../assets/content-fragment-create.png)
1. 点按或单击确认窗口中的&#x200B;**打开**。

   ![内容片段已创建确认](../assets/content-fragment-confirmation.png)
1. 在内容片段编辑器中提供内容片段的详细信息。

   ![内容片段编辑器](../assets/content-fragment-edit.png)
1. 点按或单击&#x200B;**保存并关闭**。

内容片段可以引用其他内容片段，从而允许在必要时使用嵌套的内容结构。

内容片段还可以引用AEM中的其他资产。 [创建引用内容片段之前，](/help/assets/manage-digital-assets.md) 这些资产需要存储在AEM中。

## 后续步骤{#next-steps}

现在您已创建内容片段，您可以继续阅读入门指南的最后一部分，并[创建API请求以访问和传送内容片段。](create-api-request.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/assets/content-fragments/content-fragments.md)
