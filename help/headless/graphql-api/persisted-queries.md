---
title: 持久 GraphQL 查询
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中使用持久 GraphQL 查询优化性能。持久查询可以由客户端应用程序使用 HTTP GET 方法请求，响应可以缓存在 Dispatcher 和 CDN 层中，最终改进客户端应用程序的性能。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 368c2d537d740b2126aa7cce657ca54f7ad6b329
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 94%

---

# 持久 GraphQL 查询 {#persisted-queries-caching}

持久查询是创建并存储在 Adobe Experience Manager (AEM) as a Cloud Service 服务器上的 GraphQL 查询。它们可以经客户端应用程序以 GET 请求方式请求。GET 请求的响应可以在 Dispatcher 和 CDN 层缓存，最终改进请求客户端应用程序的性能。这与标准的 GraphQL 查询不同，后者使用 POST 请求执行，而在 POST 请求中，无法轻松缓存响应。

>[!NOTE]
>
>建议使用持久查询。 请参阅 [GraphQL查询最佳实践(Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) 以了解详细信息和相关的Dispatcher配置。

的 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) 可在AEM中开发、测试和保留GraphQL查询，之后即可 [转移到生产环境](#transfer-persisted-query-production). 对于需要自定义的情况（例如，当[自定义缓存](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)），您可以使用该 API；请参阅[“如何持久 GraphQL 查询”](#how-to-persist-query)中提供的 CURL 示例。

## 持久查询及端点 {#persisted-queries-and-endpoints}

持久查询必须始终使用与[相应 Sites 配置](graphql-endpoint.md)相关的端点，因此它们可以使用以下项之一或全部：

* 全球配置和端点
查询具有对所有内容片段模型的访问权限。
* 特定 Sites 配置和端点
为特定 Sites 配置创建持久查询需要对应的 Sites 配置特定的端点（用于提供对相关内容片段模型的访问权限）。
例如，要创建特定于 WKND Sites 配置的持久查询，必须预先创建对应的 WKND 特定的端点。

>[!NOTE]
>
>有关更多详细信息，请参阅[在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
>
>对于适当的 Sites 配置，需要启用&#x200B;**GraphQL 持久查询**。

例如，如果存在名为 `my-query` 的特定查询，使用来自 Sites 配置 `my-conf` 的模型 `my-model`：

* 您可以使用 `my-conf` 特定的端点创建查询，然后查询将保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端点创建相同的查询，但然后查询将保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这里有两种不同的查询，保存在不同的路径中。
>
>它们只是正好使用了相同的模型，但通过不同的端点。

## 如何使 GraphQL 查询持久 {#how-to-persist-query}

建议先在 AEM 作者环境中保留查询，然后将[查询转移到](#transfer-persisted-query-production) AEM 发布环境中，供应用程序使用。

有多种持久查询的方法，包括：

* GraphiQL IDE - 请参阅[“保存持久查询”](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* CURL - 请查看以下示例
* 其他工具，包括 [Postman](https://www.postman.com/)

以下提供了一些步骤，介绍使用 **curl** 命令行工具使指定查询持久。

1. 使用 PUT 操作将查询放入新端点 URL `/graphql/persist.json/<config>/<persisted-label>` 来准备查询。

   例如，创建持久查询：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此时，检查响应。

   例如，检查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，您可以通过对 URL `/graphql/execute.json/<shortPath>` 执行 GET 操作来请求持久查询。

   例如，使用持久查询：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过将持久查询 POST 到已经存在的查询路径来更新持久查询。

   例如，使用持久查询：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 创建打包的简单查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控制创建打包的简单查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用参数创建持久查询：

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 使用参数执行查询。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## 正在将持久查询转移到生产环境  {#transfer-persisted-query-production}

最终，您的持久查询需要在您的 (AEM as a Cloud Service) 生产发布环境中，可供客户端应用程序请求。要在生产发布环境中使用持久查询，需要复制相关的持久树：

* 最初是移至生产作者环境，以供通过查询来验证新撰写的内容。
* 最后移至生产发布环境，以供实时使用。

有几种转移您的持久查询的方法：

1. 使用包：
   1. 创建新的包定义。
   1. 包括配置（例如，`/conf/wknd/settings/graphql/persistentQueries`）。
   1. 构建包。
   1. 转移包（下载/上载或复制）。
   1. 安装包。

1. 使用 POST 进行复制：

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

一旦查询配置在生产环境中的发布环境中，同样的验证原则也适用，只需使用发布端点即可。

>[!NOTE]
>
>对于匿名访问，系统假设 ACL 允许“所有人”可以访问查询配置。
>
>如果不是这种情况，它将无法执行。

## 为应用程序使用的查询 URL 编码 {#encoding-query-url}

应用程序使用的 URL 中的任何分号 (&quot;;&quot;) 均需要编码。

例如，在请求中执行持久查询：

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

要在客户端应用程序中使用持久查询，应使用 AEM Headless 客户端 SDK：[用于 JavaScript 的 AEM Headless 客户端](https://github.com/adobe/aem-headless-client-js)。