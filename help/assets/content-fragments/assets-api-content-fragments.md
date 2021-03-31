---
title: Adobe Experience Manager作为资产HTTP API中的Cloud Service内容片段支持
description: 了解资产HTTP API中对内容片段的支持，这是AEM无头投放功能的重要部分。
feature: 内容片段，资产HTTP API
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 2%

---


# AEM Assets HTTP API 中的内容片段支持 {#content-fragments-support-in-aem-assets-http-api}

## 概述 {#overview}

了解资产HTTP API中对内容片段的支持，这是AEM无头投放功能的重要部分。

>[!NOTE]
>
>[资产HTTP API](/help/assets/mac-api-assets.md)包含：
>
>* 资产REST API
>* 包括对内容片段的支持

>
>
资产HTTP API的当前实现基于[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)体系结构样式。

[资产REST API](/help/assets/mac-api-assets.md)允许开发人员将Adobe Experience Manager作为Cloud Service，通过CRUD操作（创建、读取、更新、删除）直接通过HTTP API访问内容(存储在AEM中)。

通过向JavaScript前端应用程序提供内容服务，API允许您将Adobe Experience Manager作为无外设CMS(内容管理系统)的Cloud Service进行操作。 或可以执行HTTP请求并处理JSON响应的任何其他应用程序。

例如，单页应用程序(SPA)（基于框架或自定义）需要通过HTTP API提供的内容，通常采用JSON格式。

虽然[AEM核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)提供了一个非常全面、灵活且可自定义的API，可用于执行所需的读取操作，并且可以自定义其JSON输出，但它们确实需要AEM WCM(Web内容管理)专业知识来实现，因为它们必须托管在基于专用AEM模板的页面中。 并非每个SPA开发组织都能直接获取此类知识。

此时，可以使用资产REST API。 它允许开发人员直接访问资产（例如图像和内容片段），而无需先将资产嵌入页面，然后以序列化JSON格式交付其内容。

>[!NOTE]
>
>无法从Assets REST API自定义JSON输出。

Assets REST API还允许开发人员通过创建新资产、更新或删除现有资产、内容片段和文件夹来修改内容。

资产REST API:

* 遵循[HATEOAS原则](https://en.wikipedia.org/wiki/HATEOAS)

* 实现[SIREN格式](https://github.com/kevinswiber/siren)

## 前提条件 {#prerequisites}

Assets REST API可在最近Adobe Experience Manager的每次现成安装中作为Cloud Service版本提供。

## 重要概念 {#key-concepts}

资产REST API优惠对存储在AEM实例中的资产进行[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)样式访问。

它使用`/api/assets`端点，并需要资产的路径才能访问它（没有前导`/content/dam`）。

* 这意味着要访问以下位置的资产：
   * `/content/dam/path/to/asset`
* 您需要请求：
   * `/api/assets/path/to/asset`

例如，要访问`/content/dam/wknd/en/adventures/cycling-tuscany`，请求`/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>访问：
>
>* `/api/assets` **不** 需要使用选择 `.model` 器。
>* `/content/path/to/page` **不** 需要使用选择 `.model` 器。


HTTP方法确定要执行的操作：

* **GET**  — 检索资产或文件夹的JSON表示形式
* **POST**  — 创建新资产或文件夹
* **PUT**  — 更新资产或文件夹的属性
* **DELETE**  — 删除资产或文件夹

>[!NOTE]
>
>请求体和/或URL参数可用于配置其中的一些操作；例如，定义应由&#x200B;**POST**&#x200B;请求创建文件夹或资产。

[API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)文档中定义了支持请求的确切格式。

### 事务行为{#transactional-behavior}

所有请求都是原子的。

这意味着后续(`write`)请求不能合并到单个事务中，该事务可能作为单个实体成功或失败。

### AEM(Assets)REST API与AEM组件{#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspect</td>
   <td>资产REST API<br/> </td>
   <td>AEM Component<br/>（使用Sling Models的组件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支持的用例</td>
   <td>一般用途。</td>
   <td><p>已针对单页应用程序(SPA)或任何其他（内容消耗）上下文中的使用情况进行优化。</p> <p>还可以包含布局信息。</p> </td>
  </tr>
  <tr>
   <td>支持的操作</td>
   <td><p>创建、读取、更新、删除。</p> <p>根据实体类型，包含其他操作。</p> </td>
   <td>只读.</td>
  </tr>
  <tr>
   <td>访问</td>
   <td><p>可以直接访问。</p> <p>使用映射到<code>/content/dam</code>（在存储库中）的<code>/api/assets </code>终结点。</p> 
   <p>示例路径如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要通过AEM页面上的AEM组件进行引用。</p> <p>使用<code>.model</code>选择器创建JSON表示形式。</p> <p>示例路径如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全</td>
   <td><p>可能有多个选项。</p> <p>OAuth被提出来；可以与标准设置分开配置。</p> </td>
   <td>使用AEM标准设置。</td>
  </tr>
  <tr>
   <td>建筑评论</td>
   <td><p>写访问通常会处理一个作者实例。</p> <p>读取也可以定向到发布实例。</p> </td>
   <td>由于此方法是只读的，因此它通常用于发布实例。</td>
  </tr>
  <tr>
   <td>输出</td>
   <td>基于JSON的SIREN输出：详细，但功能强大。 允许在内容中导航。</td>
   <td>基于JSON的专有输出；可通过Sling Model进行配置。 导航内容结构很难实现（但不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全 {#security}

如果在环境中使用资产REST API时没有特定的身份验证要求，则需要正确配置AEM CORS筛选器。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* [CORS/AEM解释](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [视频 — 使用AEM为CORS开发](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



在具有特定身份验证要求的环境中，建议使用OAuth。

## 可用功能{#available-features}

内容片段是资产的特定类型，请参阅[使用内容片段](/help/assets/content-fragments/content-fragments.md)。

有关通过API提供的功能的更多信息，请参阅：

* [资产REST API](/help/assets/mac-api-assets.md)
* [实体类型](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)，其中说明了特定于每个支持类型的功能（与内容片段相关）

### 分页{#paging}

资产REST API支持通过URL参数进行分页(对于GET请求):

* `offset`  — 要检索的第一个（子）实体的编号
* `limit`  — 返回的最大实体数

响应将包含分页信息，作为SIREN输出的`properties`部分的一部分。 此`srn:paging`属性包含请求中指定的（子）实体(`total`)总数、偏移量和限制(`offset`、`limit`)。

>[!NOTE]
>
>分页通常应用于容器实体（即，与请求实体的子实体相关的文件夹或具有演绎版的资产）。

#### 示例：分页{#example-paging}

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

## 实体类型{#entity-types}

### 文件夹 {#folders}

文件夹用作资产和其他文件夹的容器。 它们反映了AEM内容存储库的结构。

资产REST API公开了对文件夹属性的访问权限；例如，其名称、标题等。 资产会作为文件夹和子文件夹的子实体进行显示。

>[!NOTE]
>
>根据子资产和文件夹的资产类型，子实体的列表可能已包含定义相应子实体的完整属性集。 或者，对于子实体的此列表中的实体，只能公开减少的属性集。

### 资产 {#assets}

如果请求资产，响应将返回其元数据；，如标题、名称和由相应资产模式定义的其他信息。

资产的二进制数据会作为`content`类型的SIREN链接公开。

资产可以有多个演绎版。 它们通常作为子实体公开，一个例外是缩略图再现，它作为类型`thumbnail`(`rel="thumbnail"`)的链接公开。

### 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊的资产类型。 它们可用于访问结构化数据，如文本、数字、日期等。

由于&#x200B;*standard*&#x200B;资产（如图像或音频）存在若干差异，因此处理这些资产时会应用一些其他规则。

#### 表示{#representation}

内容片段：

* 请勿公开任何二进制数据。
* 完全包含在JSON输出中（在`properties`属性中）。

* 也被视为原子，即作为片段属性的一部分与作为链接或子实体公开元素和变量。 这允许有效访问片段的有效负荷。

#### 内容模型和内容片段{#content-models-and-content-fragments}

目前，定义内容片段结构的模型不会通过HTTP API公开。 因此，*消费者*&#x200B;需要了解片段的模型（至少是最小值） — 尽管大多数信息可以从负载推断出来；数据类型等。 是定义的一部分。

要创建新内容片段，必须提供模型的（内部存储库）路径。

#### 关联的内容 {#associated-content}

关联的内容当前未公开。

## 使用 {#using}

使用情况可能因您使用AEM作者还是发布环境以及您的特定用例而异。

* 强烈建议将创建绑定到作者实例（[，目前没有方法使用此API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)复制片段以发布）。
* 投放可以同时从两者进行，因为AEM仅以JSON格式提供所请求的内容。

   * 来自AEM作者实例的存储和投放应足以用于防火墙后的媒体库应用程序。

   * 对于实时Web投放，建议使用AEM发布实例。

>[!CAUTION]
>
>AEM云实例上的调度程序配置可能会阻止对`/api`的访问。

>[!NOTE]
>
>有关详细信息，请参阅[API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)。 特别是[Adobe Experience Manager Assets API - Content Fragments](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

### 读/投放{#read-delivery}

使用方式：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

响应是序列化JSON，其内容结构如内容片段中所示。 引用作为引用URL提供。

有两种读取操作：

* 按路径读取特定内容片段，这将返回内容片段的JSON表示形式。
* 按路径读取内容片段的文件夹：这将返回文件夹中所有内容片段的JSON表示形式。

### 创建 {#create}

使用方式：

`POST /{cfParentPath}/{cfName}`

主体必须包含要创建的内容片段的JSON表示形式，包括应在内容片段元素上设置的任何初始内容。 必须设置`cq:model`属性，并且必须指向有效的内容片段模型。 否则将导致错误。 还必须添加一个设置为`application/json`的标题`Content-Type`。

### 更新 {#update}

使用方式为

`PUT /{cfParentPath}/{cfName}`

主体必须包含要为给定内容片段更新的内容的JSON表示形式。

这只能是内容片段、单个元素或所有元素值和/或元数据的标题或描述。

### 删除 {#delete}

使用方式：

`DELETE /{cfParentPath}/{cfName}`

## 限制 {#limitations}

存在一些限制：

* **当前不支持内容片段模型**:无法读取或创建。要能够创建新内容片段或更新现有内容片段，开发人员必须知道指向内容片段模型的正确路径。 目前，只有通过管理UI才能获得这些内容的概述。
* **将忽略引用**。当前，不检查是否引用了现有内容片段。 因此，例如，删除内容片段可能会导致页面上出现包含对已删除内容片段的引用的问题。
* **JSON数据** 类型JSON数据类型的REST API输 *出当* 前基于 *字符串的输出*。

## 状态代码和错误消息{#status-codes-and-error-messages}

在相关情况下可以看到以下状态代码：

* **200** (OK)在以下情况下返回：

   * 通过`GET`请求内容片段
   * 通过`PUT`成功更新内容片段

* **201** （已创建）在以下情况下返回：

   * 通过`POST`成功创建内容片段

* **404** （未找到）在以下情况下返回：

   * 请求的内容片段不存在

* **500** （内部服务器错误）

   >[!NOTE]
   >
   >返回此错误：
   >
   >* 发生无法用特定代码标识的错误时
   >* 当给定的有效负荷无效时


   以下列表返回此错误状态时的常见情况，以及生成的错误消息（等宽）：

   * 父文件夹不存在（通过`POST`创建内容片段时）
   * 未提供内容片段模型（cq:model缺失）、无法读取（由于路径无效或权限问题）或没有有效片段模型：

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

## API参考{#api-reference}

有关详细的API参考，请参阅此处：

* [Adobe Experience Manager Assets API — 内容片段](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)

* [资产 HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#available-features)

## 其他资源 {#additional-resources}

有关更多信息，请参阅：

* [资产HTTP API文档](/help/assets/mac-api-assets.md)
* [AEM Gem会话：OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

