---
title: 创建配置无头快速开始指南
description: 作为从AEM中作为Cloud Service的无头开始的第一步，您需要创建配置。
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---


# 创建配置无头快速开始指南{#creating-configuration}

作为从AEM中作为Cloud Service的无头开始的第一步，您需要创建配置。

## 什么是配置？{#what-is-a-configuration}

配置浏览器为AEM中的配置提供通用配置API、内容结构、解析机制。

在AEM的无头内容管理环境中，将配置视为AEM内的一个工作场所，您可以创建内容模型，该模型定义将来内容和内容片段的结构。 您可以有多种配置来分离这些模型。

如果您熟悉全堆栈AEM实现中的[页面模板，](/help/sites-cloud/authoring/features/templates.md)内容模型管理配置的使用方式类似。

## 如何创建配置{#how-to-create-a-configuration}

管理员只需创建一次配置，或在组织内容模型需要新工作区时非常选择性地创建配置。 为了本入门指南的目的，我们只需创建一个配置。

1. 以Cloud Service身份登录AEM，并从主菜单中选择&#x200B;**工具->常规->配置浏览器**。
1. 为配置提供&#x200B;**标题**&#x200B;和&#x200B;**名称**。
   * **标题**&#x200B;应为描述性。
   * **名称**&#x200B;将成为存储库中的节点名称。
      * 它将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有必要，可进行调整。
1. 检查以下选项：
   * **内容片段模型**
   * **GraphQL永久查询**

   ![创建配置](../assets/create-configuration.png)

1. 点按或单击&#x200B;**创建**

您可以根据需要创建多个配置。 配置也可以嵌套。

>[!NOTE]
>
>除&#x200B;**内容片段模型**&#x200B;和&#x200B;**GraphQL永久查询**&#x200B;外，可能还需要配置选项，具体取决于您的实施要求。

## 后续步骤{#next-steps}

使用此配置，您现在可以转到入门指南的第二部分，并[创建内容片段模型。](create-content-model.md)

>[!TIP]
>
>有关配置浏览器的完整详细信息，请参阅配置浏览器文档。[](/help/implementing/developing/introduction/configurations.md)
