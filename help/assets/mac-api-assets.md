---
title: Assets HTTP API
description: 在 [!DNL Experience Manager Assets]中使用HTTP API创建、读取、更新、删除和管理数字资源。
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: 4cec40947f1b50dd627321cabfbe43033a224f8b
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] HTTP API {#assets-http-api}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

## 概述 {#overview}

[!DNL Assets] HTTP API允许对数字资源执行创建 — 读取 — 更新 — 删除(CRUD)操作，包括对元数据、演绎版和评论的操作，以及使用[!DNL Experience Manager]内容片段的结构化内容。 它在`/api/assets`中公开，并作为REST API实现。 它包括对内容片段](/help/assets/content-fragments/assets-api-content-fragments.md)的[支持。

>[!NOTE]
>
> 提供了内容片段管理API的现代化OpenAPI实施。 有关完整文档，请参阅[内容片段管理API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。 建议使用新的OpenAPI实施。 应将目前用于内容片段的Assets HTTP API迁移到新的内容片段管理OpenAPI。

要访问API，请执行以下操作：

1. 在`https://[hostname]:[port]/api.json`处打开API服务文档。
1. 关注指向`https://[hostname]:[server]/api/assets.json`的[!DNL Assets]服务链接。

API响应是适用于某些MIME类型的JSON文件，是适用于所有MIME类型的响应代码。 JSON响应是可选的，可能无法用于（例如）PDF文件。 依靠响应代码进行进一步分析或执行操作。

>[!NOTE]
>
>所有与上传或更新一般资源或二进制文件（如演绎版）相关的API调用在[!DNL Experience Manager]中作为[!DNL Cloud Service]部署已弃用。 要上载二进制文件，请改用[直接二进制上载API](developer-reference-material-apis.md#asset-upload)。

## 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊类型的资产。 它可用于访问结构化数据，如文本、数字、日期等。 由于`standard`资产（如图像或文档）存在若干差异，因此处理内容片段时适用一些其他规则。

有关详细信息，请参阅 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持。

>[!NOTE]
>
>有关可用的各种AEM API的概述以及所涉及概念的比较，请参阅[结构化内容交付和管理的API](/help/headless/apis-headless-and-content-fragments.md)。
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

## 数据模型 {#data-model}

[!DNL Assets] HTTP API公开两个主要元素：文件夹和资源（用于标准资源）。 此外，它还会为描述内容片段中结构化内容的自定义数据模型显示更详细的元素。 有关详细信息，请参阅[内容片段数据模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

>[!NOTE]
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

### 文件夹 {#folders}

文件夹与传统文件系统中的目录类似。 文件夹可以只包含资源，也可以只包含文件夹或文件夹和资源。 文件夹具有以下组件：

**实体**：文件夹的实体是其子元素，可以是文件夹和资源。

**属性**：

* `name`是文件夹的名称。 这与URL路径中没有扩展的最后一个区段相同。
* `title`是文件夹的可选标题，可以显示它而不是其名称。

>[!NOTE]
>
>文件夹或资产的某些属性映射到不同的前缀。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`前缀已替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

**链接**&#x200B;文件夹显示三个链接：

* `self`：链接到自身。
* `parent`：链接到父文件夹。
* `thumbnail`：（可选）链接到文件夹缩略图图像。

### 资源 {#assets}

在[!DNL Experience Manager]中，资产包含以下元素：

* 资源的属性和元数据。
* 最初上传的资产的二进制文件。
* 已配置多个演绎版。 这些可以是不同大小的图像、不同编码的视频，或者从PDF或[!DNL Adobe InDesign]文件中提取的页面。
* 可选注释。

有关内容片段中元素的信息，请参阅[Experience Manager Assets HTTP API中的内容片段支持](/help/assets/content-fragments/assets-api-content-fragments.md)。

>[!NOTE]
>
>[内容片段和内容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md) 也可用。

在[!DNL Experience Manager]中，文件夹具有以下组件：

* 实体：资产的子项是其演绎版。
* 属性。
* 链接。

## 可用功能 {#available-features}

[!DNL Assets] HTTP API包含以下功能：

* [检索文件夹列表](#retrieve-a-folder-listing)。
* [创建文件夹](#create-a-folder)。
* [创建资产（已弃用）](#create-an-asset)
* [更新资产二进制文件（已弃用）](#update-asset-binary)。
* [更新资源元数据](#update-asset-metadata)。
* [创建资源演绎版](#create-an-asset-rendition)。
* [更新资源演绎版](#update-an-asset-rendition)。
* [创建资产评论](#create-an-asset-comment)。
* [复制文件夹或资产](#copy-a-folder-or-asset)。
* [移动文件夹或资源](#move-a-folder-or-asset)。
* [删除文件夹、资源或演绎版](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>为了便于阅读，以下示例省略了完整的cURL符号。 表示法与[Resty](https://github.com/micha/resty)相关联，后者是cURL的脚本包装器。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 检索文件夹列表 {#retrieve-a-folder-listing}

检索现有文件夹及其子实体（子文件夹或资产）的Siren表示形式。

**请求**： `GET /api/assets/myFolder.json`

**响应代码**：响应代码为：

* 200 — 确定 — 成功。
* 404 - NOT FOUND — 文件夹不存在或无法访问。
* 500 — 内部服务器错误 — 如果出现其他错误。

**响应**：返回的实体的类是资产或文件夹。 包含的实体的属性是每个实体的完整属性集的子集。 要获取实体的完整表示形式，客户端应检索链接指向的URL的内容，该URL具有`self`的`rel`。

## 创建文件夹 {#create-a-folder}

在给定路径创建一个`sling`： `OrderedFolder`。 如果提供`*`而不是节点名称，则servlet使用参数名称作为节点名称。 请求接受以下任一情况：

* 新文件夹的警报表示形式
* 一组名称 — 值对，编码为`application/www-form-urlencoded`或`multipart`/`form`- `data`。 这些选项对于直接从HTML表单创建文件夹很有用。

此外，可以将文件夹的属性指定为URL查询参数。

如果提供的路径的父节点不存在，则API调用会失败，并返回`500`响应代码。 如果文件夹存在，调用将返回响应代码`409`。

**参数**： `name`是文件夹名称。

**请求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**响应代码**：响应代码为：

* 201 — 已创建 — 成功创建时。
* 409 — 冲突 — 如果文件夹存在。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 创建资产 {#create-an-asset}

有关如何创建资产的信息，请参阅[资产上传](developer-reference-material-apis.md)。 无法使用HTTP API创建资源。

## 更新资产二进制文件 {#update-asset-binary}

有关如何更新资产二进制文件的信息，请参阅[资产上传](developer-reference-material-apis.md)。 无法使用HTTP API更新资产二进制文件。

## 更新资源的元数据 {#update-asset-metadata}

更新资源元数据属性。 如果更新`dc:`命名空间中的任何属性，则API会更新`jcr`命名空间中的相同属性。 该API不会同步两个命名空间下的属性。

**请求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**响应代码**：响应代码为：

* 200 — 确定 — 如果已成功更新资产。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 创建资源演绎版 {#create-an-asset-rendition}

为资源创建演绎版。 如果未提供请求参数名称，则使用文件名作为演绎版名称。

**参数**：格式副本的名称为`name`，文件引用为`file`。

**请求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**响应代码**

* 201 - CREATED — 如果已成功创建呈现版本。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 更新资源演绎版 {#update-an-asset-rendition}

更新会分别用新的二进制数据替换资产演绎版。

**请求**： `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**响应代码**：响应代码为：

* 200 - OK — 如果已成功更新演绎版。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 在资产上添加评论 {#create-an-asset-comment}

**参数**：评论的消息正文的参数为`message`，JSON格式的注释数据的参数为`annotationData`。

**请求**： `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**响应代码**：响应代码为：

* 201 - CREATED — 如果评论已成功创建。
* 404 - NOT FOUND — 如果在提供的URI中找不到或无法访问资产。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 复制文件夹或资源 {#copy-a-folder-or-asset}

将提供的路径中可用的文件夹或资产复制到新目标。

**请求标头**：参数为：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity`或`0`。 使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite` — 使用`F`防止覆盖现有目标上的资产。

**请求**： `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**响应代码**：响应代码为：

* 201 - CREATED — 文件夹/资产是否已复制到不存在的目标。
* 204 — 无内容 — 如果将文件夹/资产复制到现有目标。
* 412 - PRECONDITION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 移动文件夹或资源 {#move-a-folder-or-asset}

将给定路径下的文件夹或资源移动到新目标。

**请求标头**：参数为：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity`或`0`。 使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite` — 使用`T`强制删除现有资源，或使用`F`阻止覆盖现有资源。

**请求**： `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**响应代码**：响应代码为：

* 201 - CREATED — 文件夹/资产是否已复制到不存在的目标。
* 204 — 无内容 — 如果将文件夹/资产复制到现有目标。
* 412 - PRECONDITION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 删除文件夹、资源或演绎版 {#delete-a-folder-asset-or-rendition}

在提供的路径中删除资源(-tree)。

**请求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**响应代码**：响应代码为：

* 200 - OK — 已成功删除文件夹。
* 412 - PRECONDITION FAILED — 如果找不到或无法访问根集合。
* 500 — 内部服务器错误 — 如果出现其他错误。

## 提示、最佳实践和限制 {#tips-limitations}

* 在[!UICONTROL 结束时间]后，无法通过[!DNL Assets] Web界面和HTTP API使用资产及其演绎版。 如果[!UICONTROL 开启时间]是未来的时间，或者[!UICONTROL 结束时间]是过去的时间，则API会返回404错误消息。

* Assets HTTP API不返回完整的元数据。 命名空间是硬编码的，并且只返回这些命名空间。 有关完整的元数据，请参阅资源路径`/jcr_content/metadata.json`。

* 使用API更新时，文件夹或资产的某些属性会映射到不同的前缀。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`前缀已替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

**另请参阅**

* [翻译资源](translate-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>*  [!DNL Assets]](/help/assets/developer-reference-material-apis.md)的[开发人员参考文档
