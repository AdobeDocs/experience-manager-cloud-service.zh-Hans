---
title: 创建内容片段 – Headless 设置
description: 了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: ht
source-wordcount: '348'
ht-degree: 100%

---

# 创建内容片段 – Headless 设置 {#creating-content-fragments}

了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。

## 什么是内容片段？ {#what-are-content-fragments}

[现在您已经创建了资源文件夹](create-assets-folder.md)，可以在其中存储您的内容片段，接下来可以创建片段！

您可使用内容片段设计、创建、管理和发布独立于页面的内容。利用它们，您可以准备内容以用于多个位置和多个渠道。

内容片段包含结构化内容，可以采用 JSON 格式投放。

## 如何创建内容片段 {#how-to-create-a-content-fragment}

内容作者将创建任意数量的内容片段，用于呈现他们创建的内容。这将是他们在 AEM 中的主要任务。对于本指南快速入门，我们只需要创建一个。

1. 登录 AEM as a Cloud Service，从主菜单选择&#x200B;**导航** -> **内容片段**。

1. 点按或单击[之前创建的文件夹。](create-assets-folder.md)
1. 点按或单击&#x200B;**创建**。
1. 内容片段的创建将以对话框的形式呈现。
选择要用于创建内容片段的位置和模型。

   * 可用的模型取决于您为资源文件夹](create-assets-folder.md)定义的&#x200B;[**云配置**，您将在该文件夹中创建内容片段。
   * 如果模型不可用，请检查资产文件夹的配置。

   添加标题、名称，并根据需要添加描述。

   ![创建新内容片段对话框](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. 点按或单击&#x200B;**“创建”**&#x200B;或&#x200B;**“创建并打开”**。

内容片段可以引用其他内容片段，在需要时允许嵌套内容结构。

内容片段还可以引用 AEM 中的其他资源。[这些资源需要存储在 AEM 中](/help/assets/manage-digital-assets.md)，然后才能创建引用内容片段。

## 后续步骤 {#next-steps}

现在您已经创建了内容片段，接下来可以转到快速入门指南的最后一个部分并[创建 API 请求来访问和提供内容片段。](create-api-request.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/sites-cloud/administering/content-fragments/content-fragments.md)
