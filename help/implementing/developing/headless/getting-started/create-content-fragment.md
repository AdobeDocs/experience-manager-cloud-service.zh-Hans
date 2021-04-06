---
title: 创建内容片段无头快速开始指南
description: 了解如何使用AEM内容片段设计、创建、策划和使用独立于页面的内容实现无头投放。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
translation-type: tm+mt
source-git-commit: 088fa5c90d549c52ca2832bd026be4fcddb31b78
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 创建内容片段无头快速开始指南{#creating-content-fragments}

了解如何使用AEM内容片段设计、创建、策划和使用独立于页面的内容实现无头投放。

## 什么是内容片段？{#what-are-content-fragments}

[现在，您已创建了一个资产](create-assets-folder.md) 文件夹，可以在其中存储内容片段，现在您可以创建片段！

内容片段允许您设计、创建、管理和发布独立于页面的内容。 它们允许您准备内容，准备好在多个位置和多个渠道中使用。

内容片段包含结构化内容，可以以JSON格式提供。

## 如何创建内容片段{#how-to-create-a-content-fragment}

内容作者将创建任意数量的内容片段来表示他们创建的内容。 这将是他们在AEM的主要任务。 出于本入门指南的目的，我们只需创建一个。

1. 以Cloud Service身份登录AEM，从主菜单中选择&#x200B;**导航 — >资产**。
1. 点按或单击之前创建的[文件夹。](create-assets-folder.md)
1. 点按或单击&#x200B;**创建 — >内容片段**。
1. 内容片段的创建将通过两个步骤显示为向导。 首先选择要用于创建内容片段的模型，然后点按或单击&#x200B;**下一步**。
   * 可用的模型取决于您为创建内容片段的资产文件夹](create-assets-folder.md)定义的&#x200B;[**云配置**。
   * 如果收到消息`We could not find any models`，请检查您的资产文件夹的配置。

   ![选择内容片段模型](../assets/content-fragment-model-select.png)
1. 根据需要提供&#x200B;**标题**、**说明**&#x200B;和&#x200B;**标记**，然后点按或单击&#x200B;**创建**。

   ![创建内容片段](../assets/content-fragment-create.png)
1. 点按或单击确认窗口中的&#x200B;**打开**。

   ![内容片段已创建确认](../assets/content-fragment-confirmation.png)
1. 在内容片段编辑器中提供内容片段的详细信息。

   ![内容片段编辑器](../assets/content-fragment-edit.png)
1. 点按或单击&#x200B;**保存**&#x200B;或&#x200B;**保存并关闭**。

内容片段可以引用其他内容片段，从而允许在必要时使用嵌套的内容结构。

内容片段还可以引用AEM中的其他资产。 [创建引用内容片段之前，](/help/assets/manage-digital-assets.md) 这些资产需要存储在AEM中。

## 后续步骤{#next-steps}

现在，您已经创建了内容片段，可以转到入门指南的最后一部分，并[创建API请求以访问和传送内容片段。](create-api-request.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/assets/content-fragments/content-fragments.md)
