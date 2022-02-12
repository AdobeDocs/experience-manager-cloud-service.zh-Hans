---
title: 创建API请求 — 无头设置
description: 了解如何使用GraphQL API无头交付内容片段内容，以及使用AEM Assets REST API管理内容片段。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# 创建API请求 — 无头设置 {#accessing-delivering-content-fragments}

了解如何使用GraphQL API无头交付内容片段内容，以及使用AEM Assets REST API管理内容片段。

## 什么是GraphQL和资产REST API? {#what-are-the-apis}

[现在，您已创建了一些内容片段，](create-content-fragment.md) 您可以使用AEM API无头地提供它们。

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) 允许您创建访问和交付内容片段的请求。 此API提供了一组最强大的功能，用于查询和使用内容片段内容。
   * 要使用此功能， [端点需要在AEM中定义和启用](/help/headless/graphql-api/graphql-endpoint.md)，如果需要， [已安装GraphiQL界面](/help/headless/graphql-api/graphiql-ide.md).
* [资产REST API](/help/assets/content-fragments/assets-api-content-fragments.md) 允许您创建和修改内容片段（和其他资产）。

本指南的其余部分将重点介绍GraphQL访问和内容片段交付。

## 启用GraphQL端点

必须先创建GraphQL端点，然后才能使用GraphQL API。

1. 导航到 **工具**, **资产**，然后选择 **GraphQL**.
1. 选择&#x200B;**创建**。
1. 的 **创建新GraphQL端点** 对话框。 您可以在此指定：
   * **名称**:端点名称；您可以输入任何文本。
   * **使用由提供的GraphQL模式**:使用下拉菜单选择所需的配置。
1. 使用确认 **创建**.
1. 在控制台中， **路径** 现在将根据之前创建的配置显示。 这是用于执行GraphQL查询的路径。

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

有关启用的更多详细信息 [可在此处找到GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md).

## 使用带有GraphiQL的GraphQL查询内容

信息架构师需要为其渠道端点设计查询才能交付内容。 通常，每个模型的每个端点只需要考虑一次这些查询。 在本快速入门指南中，我们只需创建一个。

GraphiQL是可安装在AEM环境中的IDE。 按照 [使用GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) 以在AEM环境中安装。

1. 登录AEMas a Cloud Service并访问GraphiQL界面：
   * 例如: `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL IDE是GraphQL的浏览器内查询编辑器。 您可以使用它来构建查询以检索内容片段，以JSON形式直接交付它们。
   * 利用左侧面板，可构建查询。
   * 右侧面板会显示结果。
   * 查询编辑器具有代码完成和热键功能，可轻松执行查询。
      ![GraphiQL编辑器](../assets/graphiql.png)

1. 假设我们创建的模型名为 `person` 带字段 `firstName`, `lastName`和 `position`，我们可以构建一个简单查询，以检索内容片段的内容。

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

1. 在左侧面板中输入查询。
   ![GraphiQL查询](../assets/graphiql-query.png)

1. 单击 **执行查询** 按钮或使用 `Ctrl-Enter` 热键和结果在右侧面板中显示为JSON。
   ![GraphiQL结果](../assets/graphiql-results.png)

1. 单击 **文档** 链接（位于页面右上方）以显示上下文文档，以帮助您构建可适应您自己模型的查询。
   ![GraphiQL文档](../assets/graphiql-documentation.png)

GraphQL支持结构化查询，这些查询不仅可以定向特定数据集或单个数据对象，还可以提供对象的特定元素、嵌套结果、支持查询变量等。

GraphQL可以避免迭代API请求和过度交付，相反，允许批量交付呈现为单个API查询响应所需的确切内容。 生成的JSON可用于将数据交付到其他网站或应用程序。

## 后续步骤 {#next-steps}

就是这样！现在，您对AEM中的无外设内容管理有了基本的了解。 当然，您还可以使用更多资源来更深入地了解可用功能。

* **[内容片段](/help/assets/content-fragments/content-fragments.md)**  — 有关创建和管理内容片段的详细信息
* **[AEM Assets HTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)**  — 有关通过CRUD操作（创建、读取、更新、删除）直接通过HTTP API访问AEM内容的详细信息
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)**  — 有关如何无头提交内容片段的详细信息
