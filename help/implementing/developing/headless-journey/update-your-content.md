---
title: 如何通过AEM Assets API更新您的内容
description: 在AEM无头开发人员历程的这一部分中，了解如何使用REST API访问和更新内容片段的内容。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: c9b8e14a3beca11b6f81f2d5e5983d6fd801bf3f
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 2%

---

# 如何通过AEM Assets API {#update-your-content}更新您的内容

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无头开发人员历程的这一部分中，](overview.md)了解如何使用REST API访问和更新内容片段的内容。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何通过AEM 投放 API访问您的内容](access-your-content.md)您学会了如何通过AEM GraphQL API在AEM中访问您的无头内容，您现在应：

* 深入了解GraphQL。
* 了解AEM GraphQL API的工作原理。
* 了解一些实用的示例查询。

本文以这些基础知识为基础，因此您了解如何通过REST API更新AEM中的现有无外设内容。

## 目标 {#objective}

* **受众**:高级
* **目标**:了解如何使用REST API访问和更新内容片段的内容：
   * 介绍AEM Assets HTTP API。
   * 介绍并讨论API中的内容片段支持。
   * 说明API的详细信息。

<!--
  * Look at sample code to see how things work in practice.
-->

## 为什么需要内容片段{#why-http-api}的资产HTTP API

在无外设历程的上一阶段，您学习了如何使用AEM GraphQL API来使用查询检索内容。

那么，为什么需要另一个API?

资产HTTP API允许您&#x200B;**读取**&#x200B;内容，但也允许您&#x200B;**创建**、**更新**&#x200B;和&#x200B;**删除**&#x200B;内容 — GraphQL API无法执行的操作。

Assets REST API可在最近Adobe Experience Manager的每次现成安装中作为Cloud Service版本提供。

## 资产 HTTP API {#assets-http-api}

资产HTTP API包括：

* 资产REST API
* 包括对内容片段的支持

资产HTTP API的当前实现基于&#x200B;**REST**&#x200B;体系结构样式，允许您通过&#x200B;**CRUD**&#x200B;操作（创建、读取、更新、删除）访问内容(存储在AEM中)。

通过这些操作，API允许您通过向JavaScript前端应用程序提供内容服务，将Adobe Experience Manager作为无外设CMS(内容管理系统)的Cloud Service进行操作。 或可以执行HTTP请求并处理JSON响应的任何其他应用程序。 例如，单页应用程序(SPA)、基于框架或自定义，需要通过API提供的内容，通常采用JSON格式。

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

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

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## 资产HTTP API和内容片段{#assets-http-api-content-fragments}

内容片段用于无标题投放，内容片段是一种特殊类型的资产。 它们用于访问结构化数据，如文本、数字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用Assets REST API {#using-aem-assets-rest-api}

### 访问 {#access}

资产REST API使用`/api/assets`端点，并需要资产的路径才能访问它（没有前导`/content/dam`）。

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


### 操作 {#operation}

HTTP方法确定要执行的操作：

* **GET**  — 检索资产或文件夹的JSON表示形式
* **POST**  — 创建新资产或文件夹
* **PUT**  — 更新资产或文件夹的属性
* **DELETE**  — 删除资产或文件夹

>[!NOTE]
>
>请求体和/或URL参数可用于配置其中的一些操作；例如，定义应由&#x200B;**POST**&#x200B;请求创建文件夹或资产。

API参考文档中定义了支持请求的确切格式。

使用情况可能因您使用AEM作者还是发布环境以及您的特定用例而异。

* 强烈建议将创建绑定到作者实例（目前没有方法使用此API复制片段以发布）。
* 投放可以同时从两者进行，因为AEM仅以JSON格式提供所请求的内容。

   * 来自AEM作者实例的存储和投放应足以用于防火墙后的媒体库应用程序。

   * 对于实时Web投放，建议使用AEM发布实例。

>[!CAUTION]
>
>AEM云实例上的调度程序配置可能会阻止对`/api`的访问。

>[!NOTE]
>
>有关详细信息，请参阅API参考。 特别是[Adobe Experience Manager Assets API - Content Fragments](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

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

有关使用AEM Assets REST API的更多详细信息，您可以参考：

* Adobe Experience Manager Assets HTTP API（其他资源）
* AEM Assets HTTP API中的内容片段支持（其他资源）

## 下一步是什么{#whats-next}

现在您已完成了AEM Headless Developer历程的这一部分，您应：

* 了解AEM Assets HTTP API的基础知识。
* 了解此API中如何支持内容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

您应该继续您的AEM无头旅程，接下来查看文档[如何将一切结合在一起 — 您的应用程序和您的内容(位于AEM无头](put-it-all-together.md)中)，了解如何带入AEM无头项目并准备投入使用。

## 其他资源 {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [HATEOAS原则](https://en.wikipedia.org/wiki/HATEOAS)
* [SIREN格式](https://github.com/kevinswiber/siren)
* [资产 HTTP API](/help/assets/mac-api-assets.md)
* [内容片段REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API参考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API — 内容片段](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)
* [CORS/AEM解释](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [视频 — 使用AEM为CORS开发](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

