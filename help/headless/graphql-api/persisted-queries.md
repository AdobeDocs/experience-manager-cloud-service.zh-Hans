---
title: 持久GraphQL查询
description: 了解如何在Adobe Experience Manager中保留GraphQL查询以优化性能。 客户端应用程序可以使用HTTPGET方法来请求持久化查询，并且响应可以缓存在调度程序和CDN层，从而最终提高客户端应用程序的性能。
feature: Content Fragments,GraphQL API
source-git-commit: 0912cadeae13050c9cfc606d1c2b8f4236cd78ed
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---


# 持久GraphQL查询 {#persisted-queries-caching}

持久查询是在AEM服务器上创建并存储的GraphQL查询。 标准GraphQL查询使用POST请求执行，且响应无法轻松缓存。 持久查询可以通过客户端应用程序的GET请求来请求。 GET请求的响应可以缓存在调度程序和CDN层，最终提高请求客户端应用程序的性能。

持久化查询必须始终使用与 [相应的站点配置](graphql-endpoint.md);这样，它们就可以同时使用或同时使用这两种方法：

* 全局配置和端点查询有权访问所有内容片段模型。
* 特定站点配置和端点为特定站点配置创建持久查询时，需要相应的特定于站点配置的端点（以提供对相关内容片段模型的访问）。
例如，要专门为WKND Sites配置创建持久查询，必须提前创建相应的WKND特定Sites配置和WKND特定端点。

>[!NOTE]
>
>请参阅 [在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 以了解更多详细信息。
>
>的 **GraphQL持久性查询** 需要为相应的站点配置启用。

例如，如果存在一个名为的特定查询 `my-query`，它使用模型 `my-model` 从站点配置 `my-conf`:

* 您可以使用 `my-conf` 特定端点，则查询将保存为：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端点，但随后查询将保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这两个查询是保存在不同路径下的不同查询。
>
>他们恰巧使用了相同的模型，但是通过不同的端点。

## 如何保留GraphQL查询

建议先在AEM创作环境中保留查询，然后 [发布查询](#publish-persisted-query) 到AEM发布环境。 诸如 [邮递员](https://www.postman.com/) 或命令行工具，如 [卷曲](https://curl.se/) 中。

以下是使用 **卷曲** 命令行工具：

1. 通过将查询发送到新端点URL来准备查询 `/graphql/persist.json/<config>/<persisted-label>`.

   例如，创建一个持久查询：

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

1. 此时，请检查响应。

   例如，检查成功与否：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，您可以通过获取URL来请求保留的查询 `/graphql/execute.json/<shortPath>`.

   例如，使用持久查询：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过POSTing将持久查询更新为现有查询路径。

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

1. 创建封装的纯查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控制创建封装的纯查询。

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

## 发布保留的查询 {#publish-persisted-query}

可以将持久化查询发布到AEM发布环境，客户端应用程序可在该环境中请求这些查询。 要在发布时使用持久查询，需要复制相关的永久树。

发布保留查询的方法有以下几种：

* **使用POST进行复制**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **使用包**:
   1. 创建新的包定义。
   1. 包括配置(例如， `/conf/wknd/settings/graphql/persistentQueries`)。
   1. 构建包。
   1. 复制包。

* **使用复制/分发工具**:
   1. 转到分发工具。
   1. 为配置选择树激活(例如， `/conf/wknd/settings/graphql/persistentQueries`)。

* **使用工作流（通过工作流启动器配置）**:
   1. 定义工作流启动器规则，用于执行将在不同事件上复制配置的工作流模型（例如，创建、修改等）。

发布查询配置后，仅使用发布端点，即可应用相同的身份验证原则。

>[!NOTE]
>
>对于匿名访问，系统假定ACL允许“每个人”有权访问查询配置。
>
>如果情况并非如此，它将无法执行。

>[!NOTE]
>
>需要对URL中的任何分号(&quot;;&quot;)进行编码。
>
>例如，与执行持久查询的请求一样：
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
