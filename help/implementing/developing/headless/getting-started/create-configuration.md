---
title: 创建配置无外设快速开始指南
description: 在AEM中创建配置，作为开始使用无头设备作为Cloud Service的第一步。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---


# 创建配置无头快速开始指南{#creating-configuration}

作为开始将AEM中的无外设作为Cloud Service的第一步，您需要创建配置。

## 什么是配置？{#what-is-a-configuration}

配置浏览器为AEM中的配置提供了通用配置API、内容结构和解析机制。

在AEM中无头内容管理的上下文中，将配置视为可在AEM中创建内容模型（定义将来内容和内容片段的结构）的工作场所。 您可以有多个配置来分离这些模型。

如果您熟悉全堆栈AEM实现中的[页面模板，](/help/sites-cloud/authoring/features/templates.md)内容模型管理配置的使用方式类似。

## 如何创建配置{#how-to-create-a-configuration}

管理员只需创建一次配置，或在组织内容模型需要新工作区时非常自选。 出于本入门指南的目的，我们只需创建一个配置。

1. 以Cloud Service身份登录AEM，从主菜单中选择&#x200B;**工具 — >常规 — >配置浏览器**。
1. 为配置提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。
   * **Title**&#x200B;应为描述性。
   * **名称**&#x200B;将成为存储库中的节点名称。
      * 将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有必要，可进行调整。
1. 选中以下选项：
   * **内容片段模型**
   * **GraphQL永久查询**

   ![创建配置](../assets/create-configuration.png)

1. 点按或单击&#x200B;**创建**

您可以根据需要创建多个配置。 配置也可以嵌套。

>[!NOTE]
>
>除&#x200B;**内容片段模型**&#x200B;和&#x200B;**GraphQL永久查询**&#x200B;之外，可能还需要配置选项，具体取决于您的实施要求。

## 后续步骤{#next-steps}

使用此配置，您现在可以转到入门指南的第二部分，并[创建内容片段模型。](create-content-model.md)

>[!TIP]
>
>有关配置浏览器的完整详细信息，请参阅配置浏览器文档。](/help/implementing/developing/introduction/configurations.md)[
