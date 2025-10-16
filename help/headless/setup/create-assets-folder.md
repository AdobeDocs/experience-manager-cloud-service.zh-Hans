---
title: 创建资源文件夹 – Headless 设置
description: 使用 AEM 内容片段模型定义内容片段的结构，也就是 Headless 内容的基础。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 86%

---

# 创建资源文件夹 – Headless 设置 {#creating-an-assets-folder}

使用 AEM 内容片段模型定义内容片段的结构，也就是 Headless 内容的基础。然后，将内容片段存储在资源文件夹中。

## 什么是资源文件夹？ {#what-is-an-assets-folder}

[现在您已创建了内容片段模型](create-content-model.md)，这些模型定义了希望用于未来内容片段的结构，也许您会希望创建一些片段。

但是，您首先需要创建用于存储这些内容的资源文件夹。

资源文件夹用于[组织传统内容资源](/help/assets/manage-digital-assets.md)，例如图像和视频以及内容片段。

## 创建和配置Assets文件夹 {#create-and-configure-an-assets-folder}

管理员只需要偶尔创建文件夹，在创建内容时用于组织内容。使用Assets控制台创建新文件夹。

创建后，您需要将[配置](/help/headless/setup/create-configuration.md)应用到文件夹。 有关详细信息，请参阅[将配置应用到文件夹](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)。

您可以在创建的文件夹中创建其他子文件夹。子文件夹将继承父文件夹的&#x200B;**云配置**。但是，如果您想要使用来自其他配置的模型，则可以覆盖此项。

如果您使用本地化的站点结构，则可以在新文件夹下[创建语言根](/help/assets/translate-assets.md)。

## 后续步骤 {#next-steps}

现在您已经为内容片段创建了文件夹，接下来可以转到快速入门指南的第四部分并[创建内容片段](create-content-fragment.md)。

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/sites-cloud/administering/content-fragments/overview.md)
