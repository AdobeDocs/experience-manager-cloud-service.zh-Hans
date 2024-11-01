---
title: Assets HTTP API中的Adobe Experience Manager as a Cloud Service内容片段支持
description: 了解Assets HTTP API中对内容片段的支持，这是Adobe Experience Manager的Headless投放功能的重要组成部分。
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: 7386298ee83eef5693ce00077659bbc4a1a70d24
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 15%

---

# AEM Assets HTTP API中的内容片段支持 {#content-fragments-support-in-aem-assets-http-api}

## 概述 {#overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html) |
| AEM as a Cloud Service | 本文 |

了解Assets HTTP API中对内容片段的支持，这是Adobe Experience Manager (AEM) Headless投放功能的重要组成部分。

>[!NOTE]
>
>有关可用的各种AEM API的概述以及所涉及概念的比较，请参阅[结构化内容交付和管理的API](/help/headless/apis-headless-and-content-fragments.md)。
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md)包含：
>
>* Assets REST API
>* 包括对内容片段的支持
>
>Assets HTTP API的当前实现基于[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)架构样式。

>[!NOTE]
>
>有关 Experience Manager API 的最新信息，请访问 [Adobe Experience Manager as a Cloud Service APIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/)。

[Assets REST API](/help/assets/mac-api-assets.md)允许Adobe Experience Manager as a Cloud Service的开发者通过CRUD（创建、读取、更新、删除）操作，直接通过HTTP API访问内容(存储在AEM中)。

该API允许您通过向Adobe Experience Manager as a Cloud Service前端应用程序提供内容服务，将JavaScript作为headless CMS（内容管理系统）运行。 或任何可以执行HTTP请求并处理JSON响应的其他应用程序。

例如，[单页应用程序(SPA)](/help/implementing/developing/hybrid/introduction.md)（基于框架或自定义）需要通过HTTP API提供的内容，通常采用JSON格式。

虽然[AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)提供了一个可自定义的API，该API可为此目的提供所需的读取操作，并且可以自定义其JSON输出，但它们确实需要AEM WCM （Web内容管理）专门知识才能实现。 这是因为它们必须在基于专用AEM模板的页面中托管。 并非每个SPA开发组织都可以直接访问此类知识。

此时，可以使用Assets REST API。 它允许开发人员直接访问资产（例如图像和内容片段），而无需先将资产嵌入页面，然后以序列化JSON格式交付其内容。

>[!NOTE]
>
>无法从Assets REST API自定义JSON输出。

Assets REST API还允许开发人员通过创建新资源、更新或删除现有资源、内容片段和文件夹来修改内容。

Assets REST API：

* 遵循[HATEOAS原则](https://en.wikipedia.org/wiki/HATEOAS)

* 实施[SIREN格式](https://github.com/kevinswiber/siren)

## 先决条件 {#prerequisites}

Assets REST API 在最新版本的 Adobe Experience Manager as a Cloud Service 的每个现成安装中提供。

## 重要概念 {#key-concepts}

Assets REST API为存储在AEM实例中的资源提供[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)样式的访问权限。

它使用`/api/assets`终结点，并需要资源的路径才能访问它（没有前导`/content/dam`）。

* 这意味着，要访问以下位置的资产：
   * `/content/dam/path/to/asset`
* 请求：
   * `/api/assets/path/to/asset`

例如，要访问 `/content/dam/wknd/en/adventures/cycling-tuscany`，需要请求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>访问：
>
>* `/api/assets`**不**&#x200B;需要使用 `.model` 选择器。
>* `/content/path/to/page`**需要**&#x200B;使用 `.model` 选择器。

HTTP 方法决定了要执行的操作：

* **GET** – 检索资产或文件夹的 JSON 表示形式
* **POST** — 创建资源或文件夹
* **PUT** – 更新资产或文件夹的属性
* **DELETE** – 删除资产或文件夹

>[!NOTE]
>
>请求正文和/或 URL 参数可用于配置其中一些操作；例如，定义文件夹或资产应由 **POST** 请求创建。

支持的请求的确切格式在[API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)文档中定义。

>[!NOTE]
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

### 事务性行为 {#transactional-behavior}

所有请求都是原子的。

这意味着后续(`write`)请求无法组合为单个事务，该事务可能会作为单个实体成功或失败。

### AEM (Assets) REST API与AEM组件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>长宽比</td>
   <td>Assets REST API<br/> </td>
   <td>AEM组件<br/>（使用Sling模型的组件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支持的用例</td>
   <td>一般目的。</td>
   <td><p>针对单页应用程序(SPA)或任何其他（使用内容）上下文中的使用情况进行了优化。</p> <p>它还可以包含布局信息。</p> </td>
  </tr>
  <tr>
   <td>支持的操作</td>
   <td><p>创建、读取、更新、删除。</p> <p>附加操作，具体取决于实体类型。</p> </td>
   <td>只读。</td>
  </tr>
  <tr>
   <td>访问</td>
   <td><p>可以直接访问。</p> <p>使用映射到<code>/content/dam</code>的<code>/api/assets </code>端点（在存储库中）。</p> 
   <p>示例路径如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>必须通过AEM页面上的AEM组件引用它。</p> <p>使用<code>.model</code>选择器创建JSON表示形式。</p> <p>示例路径如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可以使用多个选项。</p> <p>建议使用OAuth；可以独立于标准设置进行配置。</p> </td>
   <td>使用AEM的标准设置。</td>
  </tr>
  <tr>
   <td>架构注释</td>
   <td><p>写访问通常针对创作实例。</p> <p>读取操作也可能定向到Publish实例。</p> </td>
   <td>由于此方法为只读，因此通常用于Publish实例。</td>
  </tr>
  <tr>
   <td>输出</td>
   <td>基于JSON的SIREN输出：冗长，但功能强大。 它允许在内容中导航。</td>
   <td>基于JSON的专有输出；可通过Sling模型配置。 导航内容结构难以实施（但并不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果在没有特定身份验证要求的环境中使用Assets REST API，则必须正确配置AEM CORS过滤器。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* [已说明 CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [视频 — 使用AEM开发CORS (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

在具有特定身份验证要求的环境中，建议使用OAuth。

## 可用功能 {#available-features}

内容片段是特定类型的资产，请参阅[使用内容片段](/help/assets/content-fragments/content-fragments.md)。

有关通过API提供的功能的更多信息，请参阅：

* [Assets REST API](/help/assets/mac-api-assets.md)
* [实体类型](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)，其中说明了特定于每个受支持类型（与内容片段相关）的功能

>[!NOTE]
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

### 分页 {#paging}

Assets REST API支持通过URL参数进行分页(对于GET请求)：

* `offset` — 要检索的第一个（子）实体的编号
* `limit` — 返回的最大实体数

响应包含作为SIREN输出`properties`部分一部分的寻呼信息。 此`srn:paging`属性包含请求中指定的（子）实体总数(`total`)、偏移量和限制(`offset`、`limit`)。

>[!NOTE]
>
>分页通常应用于容器实体（即具有演绎版的文件夹或资产），因为它与所请求实体的子项相关。

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

文件夹充当资源和其他文件夹的容器。 它们反映了AEM内容存储库的结构。

Assets REST API公开对文件夹属性的访问权限。 例如，其名称和标题。 Assets将作为文件夹和子文件夹的子实体显示。

>[!NOTE]
>
>根据子资源和文件夹的资源类型，子实体列表可能已经包含定义相应子实体的完整属性集。 或者，对于该子实体列表中的实体，只能公开缩减的属性集。

### 资源 {#assets}

如果请求资产，则响应将返回其元数据；例如标题、名称以及各个资产架构定义的其他信息。

资产的二进制数据作为类型为`content`的SIREN链接公开。

Assets可以具有多个演绎版。 这些通常作为子实体显示，一个例外是缩略图演绎版，该演绎版作为类型`thumbnail` (`rel="thumbnail"`)的链接显示。

### 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊类型的资产。 它们可用于访问结构化数据，如文本、数字、日期等。

由于与&#x200B;*标准*&#x200B;资源（如图像或音频）存在若干差异，因此处理这些资源时适用一些其他规则。

#### 呈现 {#representation}

内容片段：

* 不要公开任何二进制数据。
* 包含在JSON输出中（在`properties`属性内）。

* 它们也被认为是原子的。 也就是说，元素和变体作为片段属性的一部分显示，而不是作为链接或子实体显示。 这样可以高效地访问片段的负载。

#### 内容模型和内容片段 {#content-models-and-content-fragments}

目前，定义内容片段结构的模型不会通过HTTP API公开。 因此，*消费者*&#x200B;必须知道片段的模型（至少是最低限度） — 尽管大多数信息可以从有效负荷中推断；因为数据类型等是定义的一部分。

要创建内容片段，必须提供模型的（内部存储库）路径。

#### 关联的内容 {#associated-content}

关联内容未公开。

## 使用 {#using}

根据您使用的是AEM Author还是Publish环境，以及您的特定用例，使用情况可能会有所不同。

* 建议将创建绑定到创作实例([)，当前没有方法复制片段以使用此API发布](/help/assets/content-fragments/assets-api-content-fragments.md#limitations))。
* 可以通过这两种方式交付，因为 AEM 仅以 JSON 格式提供请求的内容。

   * 对于防火墙后的媒体库应用程序，AEM创作实例的存储和交付应已足够。

   * 对于实时Web交付，建议使用AEM Publish实例。

>[!CAUTION]
>
>AEM Cloud实例上的Dispatcher配置可能会阻止对`/api`的访问。

>[!NOTE]
>
>请参阅[API引用](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)。 具体而言，[Adobe Experience Manager Assets API – 内容片段](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)。
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

## 限制 {#limitations}

有一些限制：

* **当前不支持内容片段模型**：无法读取或创建这些模型。 为了能够创建或更新现有的内容片段，开发人员必须知道内容片段模型的正确路径。 目前，获取这些内容的概述的唯一方法是通过管理UI。
* 已忽略&#x200B;**个引用**。 当前不检查是否引用了现有的内容片段。 因此，例如，删除内容片段可能会导致包含对已删除内容片段的引用的页面出现问题。
* **JSON数据类型** *JSON数据类型*&#x200B;的REST API输出是&#x200B;*基于字符串的输出*。

## 状态代码和错误消息 {#status-codes-and-error-messages}

在相关情况下可以看到以下状态代码：

* **200** （确定）

  返回时间：

   * 通过`GET`请求内容片段
   * 通过`PUT`成功更新内容片段

* **201** （已创建）

  返回时间：

   * 通过`POST`成功创建内容片段

* **404** （未找到）

  返回时间：

   * 请求的内容片段不存在

* **500** （内部服务器错误）

  >[!NOTE]
  >
  >返回此错误：
  >
  >* 当发生无法使用特定代码标识的错误时
  >* 当给定的有效负载无效时

  下面列出了返回此错误状态以及生成的错误消息（等宽）时的常见情况：

   * 父文件夹不存在（通过`POST`创建内容片段时）
   * 未提供内容片段模型（缺少cq：model）、无法读取（由于路径无效或权限问题）或没有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * 无法创建内容片段（可能是权限问题）：

      * `Could not create content fragment`

   * 无法更新标题和/或描述：

      * `Could not set value on content fragment`

   * 无法设置元数据：

      * `Could not set metadata on content fragment`

   * 找不到内容元素或无法更新内容元素

      * `Could not update content element`
      * `Could not update fragment data of element`

  通过以下方式返回详细的错误消息：

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

## API 引用 {#api-reference}

有关详细的API参考，请参阅此处：

* [Adobe Experience Manager Assets API – 内容片段](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#available-features)

* [内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

## 其他资源 {#additional-resources}

有关更多信息，请参阅:

* [Assets HTTP API文档](/help/assets/mac-api-assets.md)
* [AEM Gem会话： OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html)
