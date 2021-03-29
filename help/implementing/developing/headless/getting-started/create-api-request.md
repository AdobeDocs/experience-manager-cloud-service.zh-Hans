---
title: 访问和交付内容片段无头快速开始指南
description: 了解如何使用AEM Assets REST API管理内容片段和GraphQL API来无外设投放内容片段内容。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# 访问和传送内容片段无头快速开始指南{#accessing-delivering-content-fragments}

了解如何使用AEM Assets REST API管理内容片段和GraphQL API来无外设投放内容片段内容。

## 什么是GraphQL和Assets REST API?{#what-are-the-apis}

[现在您已创建了一些内容片段，](create-content-fragment.md) 您可以使用AEM API无头地提供它们。

* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) 允许您创建访问和传送内容片段的请求。
* [资产REST API允](/help/assets/content-fragments/assets-api-content-fragments.md) 许您创建和修改内容片段（和其他资产）。

本指南的其余部分将重点介绍GraphQL访问和内容片段投放。

## 如何使用GraphQL {#how-to-deliver-a-content-fragment}传送内容片段

信息架构师需要为其渠道端点设计查询，以便提供内容。 通常，每个模型的每个端点只需考虑一次这些查询。 出于本入门指南的目的，我们只需创建一个。

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. 以Cloud Service身份登录AEM并访问GraphicQL界面：
   * 例如：`https://<host>:<port>/content/graphiql.html`。

1. GraphiQL是GraphQL的浏览器内查询编辑器。 您可以使用它构建查询来检索内容片段，以JSON形式直接提供它们。
   * 使用左面板可构建查询。
   * 右侧面板显示结果。
   * 查询编辑器具有代码完成和热键功能，可轻松执行查询。
      ![图形QL编辑器](../assets/graphiql.png)

1. 假设我们创建的模型名为`person`（字段为`firstName`、`lastName`和`position`），我们可以构建一个简单的查询来检索内容片段的内容。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 在左面板中输入查询。
   ![图形QL查询](../assets/graphiql-query.png)

1. 单击&#x200B;**执行查询**&#x200B;按钮或使用`Ctrl-Enter`热键，结果将在右侧面板中显示为JSON。
   ![GraphiQL结果](../assets/graphiql-results.png)

1. 单击页面右上角的&#x200B;**Docs**链接可显示上下文文档，帮助您构建适应于您自己的模型的查询。
   ![GraphiQL文档](../assets/graphiql-documentation.png)

GraphQL支持结构化查询，不仅可以目标特定数据集或单个数据对象，还可以提供对象的特定元素、嵌套结果、优惠对查询变量的支持等。

GraphQL可以避免迭代API请求和过度投放，而且允许批量投放渲染所需的具体内容，作为对单个API查询的响应。 生成的JSON可用于向其他网站或应用程序提供数据。

## 后续步骤{#next-steps}

就这样！ 您现在对AEM中的无头内容管理有了基本的了解。 当然，您可以更深入地了解更多资源，以全面了解可用功能。

* **配置浏览器**  — 有关AEM配置浏览器的详细信息
* **[内容片段](/help/assets/content-fragments/content-fragments.md)**  — 有关创建和管理内容片段的详细信息
* **[AEM Assets HTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)**  — 有关通过HTTP API直接访问AEM内容的详细信息，请通过CRUD操作（创建、读取、更新、删除）
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  — 有关如何无头传送内容片段的详细信息
