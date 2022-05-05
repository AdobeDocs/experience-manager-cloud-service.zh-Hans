---
title: 在 AEM 中使用 GraphiQL IDE
description: 了解如何在 Adobe Experience Manager 中使用 GraphiQL IDE。
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 5f0221fad6086f8d5c5e9bd5164d05ea8d6e7d2c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 98%

---

# 使用 GraphiQL IDE {#graphiql-ide}

标准 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE 的实施可与 Adobe Experience Manager (AEM) as a Cloud Service 的 GraphQL API 一起使用。

>[!NOTE]
>
>该功能的部分功能在预发布渠道中提供。特别是与持久查询相关的功能。
> 
>有关如何为您的环境启用该功能的信息，请参阅[预发布渠道文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease)。

>[!NOTE]
>
>GraphiQL 包含在 AEM 中，但默认情况下，它仅在`dev-authors`环境中启用。

>[!NOTE]
>在使用 GraphiQL IDE 之前，您必须在 [配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md) 中 [配置您的端点](/help/headless/graphql-api/graphql-endpoint.md)。


**GraphiQL** 工具允许您测试和调试 GraphQL 查询，方法是：
* 选择适用于您要用于查询的 Sites 配置的&#x200B;**端点**
* 直接输入新查询
* 创建并访问&#x200B;**[持久查询](/help/headless/graphql-api/persisted-queries.md)**
* 运行查询以立即查看结果
* 管理&#x200B;**查询变量**
* 保存并管理&#x200B;**持久查询**
* 发布或取消发布&#x200B;**持久查询**（到/从 `dev-publish`）
* 请参阅之前查询的&#x200B;**历史记录**
* 使用&#x200B;**文档资源管理器**&#x200B;访问文档；帮助您学习和理解可用的方法。

您可以通过以下任一方式访问查询编辑器：

* **工具** -> **常规** -> **GraphQL查询编辑器**
* 直接；例如， `http://localhost:4502/aem/graphiql.html`

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

您可以在开发作者系统上使用 GraphiQL，以便客户端应用程序可以使用 GET 请求和发布查询来请求 GraphiQL。对于生产使用，您必须[将查询移动到生产环境](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production)。最初是移至生产作者环境，以供通过查询来验证新撰写的内容，最后移至生产发布环境，以供实时使用。

## 选择您的端点 {#selecting-endpoint}

第一步，您需要选择您想用于查询的&#x200B;**[端点](/help/headless/graphql-api/graphql-endpoint.md)**。该端点适用于您要用于查询的 Sites 配置。

这可以从右上角的下拉列表中获得。

## 创建并持久化新查询 {#creating-new-query}

您可以在编辑器中输入新查询，该编辑器位于左中面板的 GraphiQL 徽标正下方。

>[!NOTE]
>
>如果您已经选择了一个持久查询，并显示在编辑器面板中，请选择`+`（在&#x200B;**持久查询**&#x200B;旁边）清空编辑器，为新查询做好准备。

只要开始输入，编辑器还会：

* 使用鼠标悬停显示有关元素的其他信息
* 提供语法突出显示、自动完成、自动建议等功能

>[!NOTE]
>
>GraphQL 查询通常以`{`字符开头。
>
>以`#`开头的行会被忽略。

使用&#x200B;**另存为**&#x200B;来保存新查询。

## 正在更新您的持久查询 {#updating-persisted-query}

从&#x200B;**持久查询**&#x200B;面板（最左边）的列表中选择要更新的查询。

查询将显示在编辑器面板中。进行任何需要的更改，然后使用&#x200B;**保存**&#x200B;将更新提交到持久查询。

## 正在运行查询 {#running-queries}

您可以立即运行新查询，或者加载并运行持久查询。要加载持久查询，请从列表中选择它，查询将显示在编辑器面板中。

在两种情况下，编辑器面板中显示的查询都是在以下情况下执行的查询：

* 点击/敲击&#x200B;**“执行查询”**&#x200B;图标
* 使用键盘组合`Control-Enter`

## 查询变量 {#query-variables}

<!-- more details needed here? -->

GraphiQL IDE 还允许您管理[查询变量](/help/headless/graphql-api/content-fragments.md#graphql-variables)。

例如：

![GraphQL 变量](assets/cfm-graphqlapi-03.png "GraphQL 变量")

## 发布持久查询 (dev-publish) {#publishing-persisted-queries}

一旦从列表（左面板）中选择了持久查询，您就可以使用&#x200B;**发布**&#x200B;和&#x200B;**取消发布**&#x200B;操作。这将把它们激活到您的开发发布环境 (`dev-publish`) 中，以便您的应用程序在测试时轻松访问。

>[!NOTE]
>
>持久查询缓存`Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} 定义的默认值为 2 小时（7200 秒）。

## 正在缓存您的持久查询 {#caching-persisted-queries}

AEM 将根据默认生存时间 (TTL) 使 Content Delivery Network (CDN) 缓存失效。

此值设置为：

* 7200 秒是 Dispatcher 和 CDN 的默认 TTL；也称为&#x200B;*共享缓存*
   * 默认：s-maxage=7200
* 60 是客户端（例如浏览器）的默认 TTL
   * 默认：maxage=60

使用 GraphiQL UI 持久化的 AEM GraphQL 查询在执行时将使用默认的 TTL。如果要更改 GraphLQ 查询的 TTL，则必须使用 API 方法持久查询。这涉及到在命令行界面中使用 CURL 将查询发布到 AEM。

例如：

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

可以在创建时（PUT）或以后（例如，通过 POST 请求）设置 `cache-control`。在创建持久查询时，缓存控制是可选的，因为 AEM 可以提供默认值。有关使用 CURL 持久查询的示例，请参见[如何持久化 GraphQL 查询](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query)。

## 复制 URL 以直接访问查询 {#copy-url}

**“复制 URL”**&#x200B;选项允许您通过复制用于直接访问持久查询并查看结果的 URL 来模拟查询。然后可以将其用于测试；例如，通过在浏览器中访问：

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

例如：

`http://localhost:4502/graphql/execute.json/global/article-list-01`

通过在浏览器中使用此 URL，可以确认结果：

![GraphiQL - 复制 URL ](assets/cfm-graphiql-copy-url.png "GraphiQL - 复制 URL")

**“复制 URL”**&#x200B;选项可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

![GraphiQL - 复制 URL ](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - 复制 URL")

## 正在删除持久查询 {#deleting-persisted-queries}

**“删除”**&#x200B;选项也可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

<!-- what happens if you try to delete something that is still published? -->


## 正在生产环境中安装您的持久查询 {#installing-persisted-query-production}

在使用 GraphiQL 开发和测试您的持久查询之后，最终目标是将其[转移到生产环境](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production)中，供应用程序使用。

## 键盘快捷键 {#keyboard-shortcuts}

有多种键盘快捷键可供直接访问 IDE 中的操作图标：

* 美化查询：`Shift-Control-P`
* 合并查询：`Shift-Control-M`
* 执行查询：`Control-Enter`
* 自动完成：`Control-Space`

>[!NOTE]
>
>在一些键盘上，该`Control`键被标记为`Ctrl`。
