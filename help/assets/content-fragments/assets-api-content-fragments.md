---
title: Adobe Experience Manager as a Cloud Service Assets HTTP API中的内容片段支持
description: 了解资产HTTP API中对内容片段的支持，HTTP API是AEM的一项重要无头交付功能。
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: cf8c8353d83e4446f52235a2ea1a322a84786b61
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 2%

---

# AEM Assets HTTP API 中的内容片段支持 {#content-fragments-support-in-aem-assets-http-api}

## 概述 {#overview}

了解资产HTTP API中对内容片段的支持，HTTP API是AEM的一项重要无头交付功能。

>[!NOTE]
>
>的 [资产HTTP API](/help/assets/mac-api-assets.md) 包括：
>
>* 资产REST API
>* 包括对内容片段的支持
>
>资产HTTP API的当前实施基于 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 建筑风格。

的 [资产REST API](/help/assets/mac-api-assets.md) 允许开发人员通过CRUD操作（创建、读取、更新、删除），直接通过HTTP API访问内容(存储在AEM中)。

该API允许您通过向JavaScript前端应用程序提供内容服务，将Adobe Experience Manager as a Cloud Service作为无头CMS（内容管理系统）进行操作。 或任何可以执行HTTP请求并处理JSON响应的其他应用程序。

例如， [单页应用程序(SPA)](/help/implementing/developing/hybrid/introduction.md)、基于框架或自定义的HTTP API中提供的内容，通常采用JSON格式。

While [AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 提供一个非常全面、灵活且可自定义的API，该API可为此目的提供所需的读取操作，并且其JSON输出可进行自定义，因此它们需要AEM WCM（Web内容管理）专业知识才能进行实施，因为它们必须在基于专用AEM模板的页面中托管。 并非每个SPA开发组织都能直接获取此类知识。

此时可以使用资产REST API。 它允许开发人员直接访问资产（例如，图像和内容片段），而无需先将资产嵌入到页面中，然后以序列化JSON格式交付其内容。

>[!NOTE]
>
>无法从Assets REST API自定义JSON输出。

资产REST API还允许开发人员通过创建新资产、更新或删除现有资产、内容片段和文件夹来修改内容。

资产REST API:

* 以下 [HATEOAS原则](https://en.wikipedia.org/wiki/HATEOAS)

* 实施 [SIREN格式](https://github.com/kevinswiber/siren)

## 前提条件 {#prerequisites}

在最新Adobe Experience Manager as a Cloud Service版本的每次现成安装中，都提供Assets REST API。

## 重要概念 {#key-concepts}

资产REST API提供 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)对AEM实例中存储的资产的样式访问。

它使用 `/api/assets` 端点，并且需要资产的路径才能访问该资产(不具有前导 `/content/dam`)。

* 这意味着要在以下位置访问资产：
   * `/content/dam/path/to/asset`
* 您需要请求：
   * `/api/assets/path/to/asset`

例如，要访问 `/content/dam/wknd/en/adventures/cycling-tuscany`，请求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>访问：
>
>* `/api/assets` **不** 需要使用 `.model` 选择器。
>* `/content/path/to/page` **does** 要求使用 `.model` 选择器。


HTTP方法确定要执行的操作：

* **GET**  — 检索资产或文件夹的JSON表示形式
* **POST**  — 创建新资产或文件夹
* **PUT**  — 更新资产或文件夹的属性
* **DELETE**  — 删除资产或文件夹

>[!NOTE]
>
>请求正文和/或URL参数可用于配置其中的一些操作；例如，定义文件夹或资产应由 **POST** 请求。

支持的请求的确切格式在 [API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) 文档。

### 事务性行为 {#transactional-behavior}

所有请求都是原子的。

这表示后续(`write`)请求不能合并为单个实体可能成功或失败的单个事务。

### AEM(Assets)REST API与AEM组件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>方面</td>
   <td>资产REST API<br/> </td>
   <td>AEM组件<br/> （使用Sling模型的组件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支持的用例</td>
   <td>一般用途。</td>
   <td><p>已针对单页应用程序(SPA)或任何其他（内容使用）上下文的使用情况进行了优化。</p> <p>还可以包含布局信息。</p> </td>
  </tr>
  <tr>
   <td>支持的操作</td>
   <td><p>创建、读取、更新、删除。</p> <p>根据实体类型使用其他操作。</p> </td>
   <td>只读.</td>
  </tr>
  <tr>
   <td>访问</td>
   <td><p>可以直接访问。</p> <p>使用 <code>/api/assets </code>端点，映射到 <code>/content/dam</code> （在存储库中）。</p> 
   <p>示例路径如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要在AEM页面上通过AEM组件引用。</p> <p>使用 <code>.model</code> 用于创建JSON表示形式的选择器。</p> <p>示例路径如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可以使用多个选项。</p> <p>OAuth是提出的；可以与标准设置分开配置。</p> </td>
   <td>使用AEM标准设置。</td>
  </tr>
  <tr>
   <td>建筑备注</td>
   <td><p>写访问通常将寻址创作实例。</p> <p>也可以将读取定向到发布实例。</p> </td>
   <td>由于此方法为只读方法，因此通常将用于发布实例。</td>
  </tr>
  <tr>
   <td>输出</td>
   <td>基于JSON的SIREN输出：冗长，但功能强大。 允许在内容中导航。</td>
   <td>基于JSON的专有输出；可通过Sling模型进行配置。 导览内容结构很难实现（但不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果在没有特定身份验证要求的环境中使用AEM REST API，则需要正确配置Assets CORS筛选器。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* [CORS/AEM说明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [视频 — 使用AEM开发CORS](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
>


在具有特定身份验证要求的环境中，建议使用OAuth。

## 可用功能 {#available-features}

内容片段是一种特定类型的资产，请参阅 [使用内容片段](/help/assets/content-fragments/content-fragments.md).

有关通过API提供的功能的更多信息，请参阅：

* 的 [资产REST API](/help/assets/mac-api-assets.md)
* [实体类型](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)，其中说明了特定于每个受支持类型的功能（与内容片段相关）

### 分页 {#paging}

GETREST API支持通过URL参数进行分页（对于资产请求）：

* `offset`  — 要检索的第一个（子）实体的编号
* `limit`  — 返回的最大实体数

响应将包含作为 `properties` 部分。 此 `srn:paging` 属性包含（子）实体总数( `total`)、偏移和限制( `offset`, `limit`)。

>[!NOTE]
>
>分页通常应用于容器实体（即具有演绎版的文件夹或资产），因为它与所请求实体的子实体相关。

#### 示例：分页 {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## 实体类型 {#entity-types}

### 文件夹 {#folders}

文件夹用作资产和其他文件夹的容器。 它们反映了AEM内容存储库的结构。

资产REST API公开了对文件夹属性的访问权限；例如，其名称、标题等。 资产会作为文件夹和子文件夹的子实体显示。

>[!NOTE]
>
>根据子资产和文件夹的资产类型，子实体列表可能已包含定义相应子实体的完整属性集。 或者，对于此子实体列表中的实体，只能显示缩减的属性集。

### 资源 {#assets}

如果请求资产，响应将返回其元数据；例如标题、名称和由相应资产架构定义的其他信息。

资产的二进制数据将作为类型的SIREN链接公开 `content`.

资产可以有多个演绎版。 它们通常作为子实体显示，其中一个例外是缩略图呈现，以类型的链接显示 `thumbnail` ( `rel="thumbnail"`)。

### 内容片段 {#content-fragments}

A [内容片段](/help/assets/content-fragments/content-fragments.md) 是一种特殊类型的资产。 它们可用于访问结构化数据，例如文本、数字、日期等。

由于 *标准* 资产（例如图像或音频）中的“隐藏主体”和“显示主体”选项，则处理这些资产时会应用一些其他规则。

#### 表示 {#representation}

内容片段：

* 请勿公开任何二进制数据。
* 完全包含在JSON输出中(在 `properties` 属性)。

* 也被视为原子，即元素和变量作为片段属性的一部分公开，而作为链接或子实体公开。 这允许有效访问片段的有效负载。

#### 内容模型和内容片段 {#content-models-and-content-fragments}

当前，定义内容片段结构的模型不会通过HTTP API公开。 因此， *消费者* 需要了解片段的模型（至少是一个最小值） — 尽管大多数信息都可以从负载中推断出来；数据类型等。 是定义的一部分。

要创建新的内容片段，必须提供模型的（内部存储库）路径。

#### 关联的内容 {#associated-content}

关联的内容当前未公开。

## 使用 {#using}

用法可能因您使用的是AEM创作环境还是发布环境以及特定用例而异。

* 强烈建议将创建绑定到创作实例([目前，没有方法使用此API复制要发布的片段](/help/assets/content-fragments/assets-api-content-fragments.md#limitations))。
* 可以同时从两者进行交付，因为AEM仅以JSON格式提供请求的内容。

   * 从AEM创作实例进行存储和交付应足以在防火墙后部署媒体库应用程序。

   * 对于实时Web交付，建议使用AEM发布实例。

>[!CAUTION]
>
>AEM云实例上的调度程序配置可能会阻止访问 `/api`.

>[!NOTE]
>
>有关更多详细信息，请参阅 [API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). 特别是， [Adobe Experience Manager Assets API — 内容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).

## 限制 {#limitations}

存在以下几个限制：

* **当前不支持内容片段模型**:无法读取或创建它们。 为了能够创建新内容片段或更新现有内容片段，开发人员必须知道内容片段模型的正确路径。 目前，获取这些内容概述的唯一方法是通过管理UI。
* **引用被忽略**. 当前，没有检查是否引用了现有内容片段。 因此，例如，删除内容片段可能会导致页面上出现包含对已删除内容片段的引用的问题。
* **JSON数据类型** 的REST API输出 *JSON数据类型* 当前 *基于字符串的输出*.

## 状态代码和错误消息 {#status-codes-and-error-messages}

在相关情况下，可以看到以下状态代码：

* **200** （确定）

   返回时间：

   * 通过请求内容片段 `GET`
   * 通过成功更新内容片段 `PUT`

* **201** （已创建）

   返回时间：

   * 通过成功创建内容片段 `POST`

* **404** （未找到）

   返回时间：

   * 请求的内容片段不存在

* **500** （内部服务器错误）

   >[!NOTE]
   >
   >返回以下错误：
   >
   >* 当发生无法用特定代码标识的错误时
   >* 给定有效负载无效时


   下面列出了返回此错误状态时的常见情况，以及生成的错误消息（等宽）：

   * 父文件夹不存在（通过创建内容片段时） `POST`)
   * 未提供内容片段模型（缺少cq:model）、无法读取（由于路径无效或权限问题）或没有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * 无法创建内容片段（可能是权限问题）：

      * `Could not create content fragment`
   * 无法更新标题和描述：

      * `Could not set value on content fragment`
   * 无法设置元数据：

      * `Could not set metadata on content fragment`
   * 找不到或无法更新内容元素

      * `Could not update content element`
      * `Could not update fragment data of element`

   详细的错误消息通常以下列方式返回：

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API参考 {#api-reference}

有关详细的API参考，请参阅此处：

* [Adobe Experience Manager Assets API — 内容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [资源 HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#available-features)

## 其他资源 {#additional-resources}

有关更多信息，请参阅：

* [资产HTTP API文档](/help/assets/mac-api-assets.md)
* [AEM Gem会议：OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
