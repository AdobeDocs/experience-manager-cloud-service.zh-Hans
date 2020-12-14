---
title: 访问和交付内容片段无头快速开始指南
description: 资产REST API允许管理内容片段，而GraphQL API允许对内容片段内容进行简单的无头投放。
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 访问和交付内容片段无头快速开始指南{#accessing-delivering-content-fragments}

资产REST API允许管理内容片段，而GraphQL API允许对内容片段内容进行简单的无头投放。

## 什么是GraphQL和资产REST API?{#what-are-the-apis}

[现在您已创建了一些内容片段，](create-content-fragment.md) 可以使用AEM API无头地提供它们。

* [GraphQL API允](/help/assets/content-fragments/graphql-api-content-fragments.md) 许您创建访问和传送内容片段的请求。
* [资产REST API允](/help/assets/content-fragments/assets-api-content-fragments.md) 许您创建和修改内容片段（和其他资产）。

本指南的其余部分将重点介绍GraphQL访问和内容片段投放。

## 如何使用GraphQL {#how-to-deliver-a-content-fragment}传送内容片段

信息架构师需要为其查询端点设计渠道，以便提供内容。 通常，每个模型的每个端点只需考虑一次这些查询。 为了本入门指南的目的，我们只需创建一个。

1. 以Cloud Service身份登录AEM，并从主菜单中选择&#x200B;**工具->资产-> GraphQL**
   * 或者，也可以直接在`https://<host>:<port>/content/graphiql.html`打开页面。

1. GraphiQL是GraphQL的浏览器内查询编辑器。 您可以使用它构建查询来检索内容片段，以JSON形式直接提供它们。
   * 左侧面板允许您构建查询。
   * 右面板显示结果。
   * 查询编辑器具有代码完成和热键功能，可轻松执行查询。
      ![GraphiQL编辑器](../assets/graphiql.png)

1. 假设我们创建的模型名为`person`，字段为`firstName`、`lastName`和`position`，我们可以构建一个简单的查询来检索内容片段的内容。

   ```text
   query {
     persons {
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
   ![GraphiQL查询](../assets/graphiql-query.png)

1. 单击&#x200B;**执行查询**&#x200B;按钮或使用`Ctrl-Enter`热键，结果将在右侧面板中显示为JSON。
   ![GraphiQL结果](../assets/graphiql-results.png)

1. 单击页面右上方的&#x200B;**Docs**链接以显示上下文文档，帮助您构建适应于您自己的模型的查询。
   ![GraphiQL文档](../assets/graphiql-documentation.png)

GraphQL支持结构化查询，不仅可以目标特定数据集或单个数据对象，还可以传送对象的特定元素、嵌套结果、优惠对查询变量的支持等。

GraphQL可以避免迭代API请求和过度投放，而且允许批量投放渲染所需的具体内容，作为对单个API查询的响应。 生成的JSON可用于向其他站点或应用程序提供数据。

## 后续步骤{#next-steps}

就这样！ 您现在对AEM的无头内容管理有了基本的了解。 当然，您还可以进一步了解更多资源，以全面了解可用功能。

* **配置浏览器** -有关AEM配置浏览器的详细信息
* **[内容片段](/help/assets/content-fragments/content-fragments.md)** -有关创建和管理内容片段的详细信息
* **[AEM AssetsHTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)** -有关通过HTTP API直接访问AEM内容的详细信息，请通过CRUD操作（创建、读取、更新、删除）
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)** -有关如何无头地交付内容片段的详细信息
