---
title: 资产 HTTP API
description: 使用 [!DNL Experience Manager Assets]中的HTTP API创建、读取、更新、删除和管理数字资产。
contentOwner: AG
feature: 资产HTTP API，API
role: Developer,Architect,Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] HTTP API {#assets-http-api}

## 概述 {#overview}

[!DNL Assets] HTTP API允许对数字资产（包括对元数据、演绎版和注释）以及使用[!DNL Experience Manager]内容片段的结构化内容执行创建读取更新删除(CRUD)操作。 它在`/api/assets`处公开，并作为REST API实施。 它包括[对内容片段](/help/assets/content-fragments/assets-api-content-fragments.md)的支持。

要访问API，请执行以下操作：

1. 在`https://[hostname]:[port]/api.json`处打开API服务文档。
1. 请按照指向`https://[hostname]:[server]/api/assets.json`的[!DNL Assets]服务链接进行操作。

API响应是某些MIME类型的JSON文件，也是所有MIME类型的响应代码。 JSON响应是可选的，可能不可用，例如PDF文件。 依赖响应代码进行进一步分析或操作。

>[!NOTE]
>
>与上传或更新资产或二进制文件相关的所有API调用（通常如演绎版）均已在[!DNL Experience Manager]部署中被弃用。 [!DNL Cloud Service]要上传二进制文件，请改用[直接二进制上传API](developer-reference-material-apis.md#asset-upload)。

## 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊类型的资产。 它可用于访问结构化数据，如文本、数字、日期等。 由于`standard`资产（如图像或文档）存在一些差异，因此处理内容片段时还有其他一些规则。

有关更多信息，请参阅 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持。

## 数据模型 {#data-model}

[!DNL Assets] HTTP API公开了两个主要元素：文件夹和资产（对于标准资产）。 此外，它还针对描述内容片段中结构化内容的自定义数据模型公开了更多详细信息元素。 有关更多信息，请参阅[内容片段数据模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

### 文件夹 {#folders}

文件夹与传统文件系统中的目录类似。 文件夹只能包含资产、文件夹或文件夹和资产。 文件夹具有以下组件：

**实体**:文件夹的实体是其子元素，子元素可以是文件夹和资产。

**属性**:

* `name` 是文件夹的名称。这与URL路径中不带扩展名的最后一个区段相同。
* `title` 是文件夹的可选标题，可以显示该标题而不是其名称。

>[!NOTE]
>
>文件夹或资产的某些属性会映射到其他前缀。 `jcr`前缀（`jcr:title`、`jcr:description`和`jcr:language`）替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

**** LinksFolders公开三个链接：

* `self`:链接到自身。
* `parent`:链接到父文件夹。
* `thumbnail`:（可选）链接到文件夹缩略图图像。

### 资产 {#assets}

在[!DNL Experience Manager]中，资产包含以下元素：

* 资产的属性和元数据。
* 最初上传资产的二进制文件。
* 配置了多个演绎版。 这些图像可以是不同大小的图像、不同编码的视频，或从PDF或[!DNL Adobe InDesign]文件中提取的页面。
* 可选注释。

有关内容片段中元素的信息，请参阅Experience Manager资产HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持。

在[!DNL Experience Manager]中，文件夹具有以下组件：

* 实体：资产的子项是其演绎版。
* 属性.
* 链接.

## 可用功能 {#available-features}

[!DNL Assets] HTTP API包含以下功能：

* [检索文件夹列表](#retrieve-a-folder-listing)。
* [创建文件夹](#create-a-folder)。
* [创建资产（已弃用）](#create-an-asset)
* [更新资产二进制文件（已弃用）](#update-asset-binary)。
* [更新资产元数据](#update-asset-metadata)。
* [创建资产演绎版](#create-an-asset-rendition)。
* [更新资产演绎版](#update-an-asset-rendition)。
* [创建资产评论](#create-an-asset-comment)。
* [复制文件夹或资产](#copy-a-folder-or-asset)。
* [移动文件夹或资产](#move-a-folder-or-asset)。
* [删除文件夹、资产或演绎版](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>为方便阅读，以下示例省略了完整的cURL注释。 符号与[Resty](https://github.com/micha/resty)相关，后者是cURL的脚本包装器。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 检索文件夹列表 {#retrieve-a-folder-listing}

检索现有文件夹及其子实体（子文件夹或资产）的警报器表示形式。

**请求**:  `GET /api/assets/myFolder.json`

**响应代码**:响应代码为：

* 200 — 好 — 成功。
* 404 — 未找到 — 文件夹不存在或无法访问。
* 500 — 内部服务器错误 — 如果其他问题出现。

**响应**:返回的实体类别是资产或文件夹。包含实体的属性是每个实体的完整属性集的子集。 为了获得实体的完整表示形式，客户端应检索链接所指向的URL内容，该链接的`rel`为`self`。

## 创建文件夹 {#create-a-folder}

创建`sling`:`OrderedFolder`。 如果提供了`*`而不是节点名称，则Servlet会使用参数名称作为节点名称。 请求接受以下任一条件：

* 新文件夹的警报表示
* 一组名称 — 值对，编码为`application/www-form-urlencoded`或`multipart`/ `form`- `data`。 这些参数对于直接从HTML表单创建文件夹非常有用。

此外，还可以将文件夹的属性指定为URL查询参数。

如果提供路径的父节点不存在，则API调用会失败，并出现`500`响应代码。 如果文件夹存在，则调用会返回响应代码`409`。

**参数**: `name` 是文件夹名称。

**请求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**响应代码**:响应代码为：

* 201 — 已创建 — 成功创建时。
* 409 — 冲突 — 如果存在文件夹。
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 创建资产 {#create-an-asset}

有关如何创建资产的信息，请参阅[资产上传](developer-reference-material-apis.md)。 您无法使用HTTP API创建资产。

## 更新资产二进制文件 {#update-asset-binary}

有关如何更新资产二进制文件的信息，请参阅[资产上传](developer-reference-material-apis.md)。 您无法使用HTTP API更新资产二进制文件。

## 更新资产的元数据 {#update-asset-metadata}

更新资产元数据属性。 如果更新`dc:`命名空间中的任何属性，则API会更新`jcr`命名空间中的相同属性。 API不会同步两个命名空间下的属性。

**请求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**响应代码**:响应代码为：

* 200 — 确定 — 如果资产已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作：
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 创建资产演绎版 {#create-an-asset-rendition}

为资产创建演绎版。 如果未提供请求参数名称，则文件名将用作格式副本名称。

**参数**:这些参数用 `name` 于呈现版本的名称， `file` 并作为文件引用。

**请求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**响应代码**

* 201 — 已创建 — 如果演绎版已成功创建。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作：
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 更新资产演绎版 {#update-an-asset-rendition}

更新后，将分别使用新的二进制数据替换资产演绎版。

**请求**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**响应代码**:响应代码为：

* 200 — 确定 — 如果演绎版已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作：
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 在资产上添加评论 {#create-an-asset-comment}

**参数**:参数用 `message` 于注释的消息正文和JSON `annotationData` 格式的注释数据。

**请求**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果注释已成功创建。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作：
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 复制文件夹或资产 {#copy-a-folder-or-asset}

将提供路径上可用的文件夹或资产复制到新目标。

**请求标头**:参数包括：

* `X-Destination` - API解决方案范围中用于将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite`  — 使用 `F` 防止覆盖现有目标处的资产。

**请求**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果文件夹/资产已复制到非现有目标。
* 204 — 无内容 — 如果文件夹/资产已复制到现有目标。
* 412 - PRECONDITATION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 移动文件夹或资产 {#move-a-folder-or-asset}

将给定路径上的文件夹或资产移动到新目标。

**请求标头**:参数包括：

* `X-Destination` - API解决方案范围中用于将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite`  — 使用强制 `T` 删除现有资源，或 `F` 防止覆盖现有资源。

**请求**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果文件夹/资产已复制到非现有目标。
* 204 — 无内容 — 如果文件夹/资产已复制到现有目标。
* 412 - PRECONDITATION失败 — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 删除文件夹、资产或演绎版 {#delete-a-folder-asset-or-rendition}

删除提供路径上的资源(-tree)。

**请求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**响应代码**:响应代码为：

* 200 — 确定 — 如果文件夹已成功删除。
* 412 - PRECONTIME FAILED — 如果找不到或访问根集合，则失败。
* 500 — 内部服务器错误 — 如果其他问题出现。

## 提示、最佳实践和限制 {#tips-limitations}

* 在[!UICONTROL 结束时间]之后，资产及其演绎版无法通过[!DNL Assets] Web界面和HTTP API使用。 如果[!UICONTROL 开启时间]将来或[!UICONTROL 结束时间]过去，则API会返回404错误消息。

* 资产HTTP API不会返回完整的元数据。 命名空间采用硬编码，只返回那些命名空间。 有关完整的元数据，请参阅资产路径`/jcr_content/metadata.json`。

* 使用API更新时，文件夹或资产的某些属性会映射到其他前缀。 `jcr`前缀（`jcr:title`、`jcr:description`和`jcr:language`）替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

>[!MORELIKETHIS]
>
>* [ [!DNL Assets]的开发人员参考文档](/help/assets/developer-reference-material-apis.md)

