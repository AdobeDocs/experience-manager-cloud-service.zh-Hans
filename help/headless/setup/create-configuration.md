---
title: 创建配置 — 无头设置
description: 在AEM as a Cloud Service中创建配置，作为开始使用无头设备的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# 创建配置 — 无头设置 {#creating-configuration}

在AEMas a Cloud Service中开始使用无头时，您需要创建配置。

## 什么是配置？ {#what-is-a-configuration}

配置浏览器为AEM中的配置提供了通用配置API、内容结构和解析机制。

在AEM中进行无头内容管理时，请将配置视为AEM中的一个工作区，您可以在其中创建内容模型，该模型定义将来内容和内容片段的结构。 您可以有多个配置来分隔这些模型。

如果您熟悉 [全栈AEM实施中的页面模板，](/help/sites-cloud/authoring/features/templates.md) 配置在内容模型管理中的用法相似。

## 如何创建配置 {#how-to-create-a-configuration}

管理员只需创建一次配置，或在组织内容模型时非常自行地创建新工作区。 在本快速入门指南中，我们只需创建一个配置。

1. 登录AEMas a Cloud Service，然后从主菜单中选择 **工具 — >常规 — >配置浏览器**.
1. 提供 **标题** 和 **名称** 的URL。
   * 的 **标题** 应具有描述性。
   * 的 **名称** 将成为存储库中的节点名称。
      * 将根据标题自动生成并根据 [AEM命名约定。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有必要，可进行调整。
1. 选中以下选项：
   * **内容片段模型**
   * **GraphQL永久查询**

   ![创建配置](../assets/create-configuration.png)

1. 点按或单击 **创建**

您可以根据需要创建多个配置。 配置也可以嵌套。

>[!NOTE]
>
>除 **内容片段模型** 和 **GraphQL永久查询** 根据您的实施要求，可能需要使用。

## 后续步骤 {#next-steps}

使用此配置，您现在可以转到快速入门指南的第二部分和 [创建内容片段模型。](create-content-model.md)

>[!TIP]
>
>有关配置浏览器的完整详细信息，请 [请参阅配置浏览器文档。](/help/implementing/developing/introduction/configurations.md)
