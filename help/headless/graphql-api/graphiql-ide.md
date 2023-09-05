---
title: 在 AEM 中使用 GraphiQL IDE
description: 了解如何在 Adobe Experience Manager 中使用 GraphiQL IDE。
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: d6b98559e7cbe5fc5bd05d9cf37225e960e668e7
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# 使用 GraphiQL IDE {#graphiql-ide}

标准 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE 的实施可与 Adobe Experience Manager (AEM) as a Cloud Service 的 GraphQL API 一起使用。

>[!NOTE]
>
>GraphiQL 包含在 AEM 的所有环境中（但只有在配置端点时才可访问/显示）。
>
>在以前的版本中，安装 GraphiQL IDE 时需要软件包。如果您已安装此软件，现可将其移除。

>[!NOTE]
>在使用 GraphiQL IDE 之前，您必须在[配置浏览器](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)中[配置您的端点](/help/headless/graphql-api/graphql-endpoint.md)。

**GraphiQL** 工具让您测试和调试 GraphQL 查询，方法是：
* 选择适用于您要用于查询的 Sites 配置的&#x200B;**端点**
* 直接输入新查询
* 创建并访问&#x200B;**[持久查询](/help/headless/graphql-api/persisted-queries.md)**
* 运行查询以立即查看结果
* 管理&#x200B;**查询变量**
* 保存并管理&#x200B;**持久查询**
* 将&#x200B;**持久查询**&#x200B;发布到您的&#x200B;**发布**&#x200B;或&#x200B;**预览**&#x200B;服务，或对其进行取消发布；例如，到/从 `dev-publish` 
* 请参阅之前查询的&#x200B;**历史记录**
* 使用&#x200B;**文档资源管理器**&#x200B;访问文档；帮助您学习和理解可用的方法。

您可以通过以下任一方式访问查询编辑器：

* **工具** -> **常规** -> **GraphQL 查询编辑器**
* 直接；例如，`http://localhost:4502/aem/graphiql.html`

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

您可以在系统上使用 GraphiQL，以便您的客户端应用程序可以使用 GET 请求来请求查询，并发布查询。对于生产使用，您可以[将查询移动到生产环境](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production)。最初是移至生产作者环境，以供通过查询来验证新撰写的内容，最后移至生产发布环境，以供实时使用。

## 选择您的端点 {#selecting-endpoint}

第一步，您需要选择您想用于查询的&#x200B;**[端点](/help/headless/graphql-api/graphql-endpoint.md)**。该端点适用于您要用于查询的 Sites 配置。

这可以从右上角的下拉列表中获得。

## 创建并持久新查询 {#creating-new-query}

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

查询会显示在编辑器面板中。进行任何需要的更改，然后使用&#x200B;**保存**&#x200B;将更新提交到持久查询。

## 正在运行查询 {#running-queries}

您可以立即运行新查询，或者加载并运行持久查询。要加载持久查询，请从列表中选择它，查询会显示在编辑器面板中。

在两种情况下，编辑器面板中显示的查询都是在以下情况下运行的查询：

* 点击/点按&#x200B;**“执行查询”**&#x200B;图标
* 使用键盘组合`Control-Enter`

## 查询变量 {#query-variables}

GraphiQL IDE 还让您管理[查询变量](/help/headless/graphql-api/content-fragments.md#graphql-variables)。

例如：

![GraphQL 变量](assets/cfm-graphqlapi-03.png "GraphQL 变量")

## 管理保留查询的缓存 {#managing-cache}

建议使用[持久查询](/help/headless/graphql-api/persisted-queries.md)，因为它们可以缓存在 Dispatcher 和 CDN 层，最终提高请求客户端应用程序的性能。默认情况下，AEM 将根据默认生存时间 (TTL) 使内容投放网络 (CDN) 缓存失效。

>[!NOTE]
>
>有关更多详细信息，请参阅[缓存您的持久查询](/help/headless/graphql-api/persisted-queries.md#caching-persisted-queries)。

>[!NOTE]
>
>Dispatcher 上的自定义重写规则可能会覆盖来自 AEM 发布的默认值。
>
>如果您根据位置匹配模式从 Dispatcher 发送基于 TTL 的缓存控制标头，则如有必要，您可能需要从匹配项中排除 `/graphql/execute.json/*`。

使用 GraphQL，您可以配置 HTTP 缓存标头，以控制单个持久查询的这些参数。

1. **标头**&#x200B;选项可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

   ![持久查询 HTTP 缓存标头](assets/cfm-graphqlapi-headers-01.png "持久查询 HTTP 缓存标头")

1. 选择此选项将打开&#x200B;**缓存配置**&#x200B;对话框：

   ![持久查询 HTTP 缓存标头设置](assets/cfm-graphqlapi-headers-02.png "持久查询 HTTP 缓存标头设置")

1. 选择相应的参数，然后根据需要调整值：

   * **cache-control** – **max-age**
缓存可以将此内容存储指定的秒数。通常为浏览器 TTL（生存时间）。
   * **surrogate-control** – **s-maxage**
与 max-age 相同，但特别适用于代理缓存。
   * **surrogate-control** – **stale-while-revalidate**
缓存可能会在缓存响应过期后继续为其提供服务，最长可达指定的秒数。
   * **surrogate-control** – **stale-if-error**
在发生源错误的情况下，缓存可以继续为缓存响应提供服务，最长可达指定的秒数。

1. 选择&#x200B;**保存**&#x200B;来保留更改。

## 发布和预览持久查询 {#publishing-previewing-persisted-queries}

一旦从列表（左面板）中选择了持久查询，您就可以使用&#x200B;**发布**&#x200B;操作。

这将会激活对您选择的环境的查询。您可以选择您的&#x200B;**发布**&#x200B;环境（例如，`dev-publish`），或者您的&#x200B;**预览**&#x200B;环境，以便您的应用程序在测试时轻松访问。

![GraphiQL - 发布持久查询 ](assets/cfm-graphiql-publish.png "GraphiQL - 发布持久查询")

>[!NOTE]
>
>持久查询缓存`Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} 定义的默认值为 2 小时（7200 秒）。

## 正在取消发布持久查询 {#unpublishing-persisted-queries}

与发布时一样，一旦从列表（左面板）中选择了持久查询，您就可以使用&#x200B;**取消发布**&#x200B;操作。

这将停用您选择的环境中的查询；即您的&#x200B;**发布**&#x200B;环境，或您的&#x200B;**预览**&#x200B;环境。

>[!NOTE]
>
>您还应确保已对客户端应用程序进行了必要的更改，以避免出现潜在问题。

## 复制 URL 以直接访问查询 {#copy-url}

**“复制 URL”**&#x200B;选项让您通过复制用于直接访问持久查询并查看结果的 URL 来模拟查询。然后可以将其用于测试；例如，通过在浏览器中访问：

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

![GraphiQL – 复制 URL ](assets/cfm-graphiql-copy-url.png "GraphiQL – 复制 URL")

**“复制 URL”**&#x200B;选项可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

![GraphiQL – 复制 URL ](assets/cfm-graphiql-persisted-query-options.png "GraphiQL – 复制 URL")

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
