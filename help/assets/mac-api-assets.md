---
title: 资产 HTTP API
description: 使用 [!DNL Experience Manager Assets]中的HTTP API创建、读取、更新、删除和管理数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 332ca27c060a46d41e4f6e891f6fd98170d10d9f
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] HTTP API  {#assets-http-api}

## 概述 {#overview}

[!DNL Assets] HTTP API允许对数字资产（包括元数据、演绎版和注释）以及使用[!DNL Experience Manager]内容片段的结构化内容执行创建 — 读取 — 更新 — 删除(CRUD)操作。 它在`/api/assets`公开，并作为REST API实现。 它包括[对内容片段](/help/assets/content-fragments/assets-api-content-fragments.md)的支持。

要访问API:

1. 打开位于`https://[hostname]:[port]/api.json`的API服务文档。
1. 按照[!DNL Assets]服务链接，指向`https://[hostname]:[server]/api/assets.json`。

API响应是某些MIME类型的JSON文件和所有MIME类型的响应代码。 JSON响应是可选的，可能不可用，例如PDF文件。 依赖响应代码进行进一步的分析或操作。

>[!NOTE]
>
>与上传或更新资产或二进制文件（如演绎版）相关的所有API调用在[!DNL Experience Manager]部署中已弃用。 [!DNL Cloud Service]对于上传二进制文件，请改用[直接二进制上传API](developer-reference-material-apis.md#asset-upload-technical)。

## 内容片段 {#content-fragments}

[内容片段](/help/assets/content-fragments/content-fragments.md)是一种特殊的资产类型。 它可用于访问结构化数据，如文本、数字、日期等。 由于`standard`资产(如图像或文档)存在多种差异，因此处理内容片段时会应用一些其他规则。

有关详细信息，请参阅 [!DNL Experience Manager Assets] HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持。

## 数据模型{#data-model}

[!DNL Assets] HTTP API公开两个主要元素、文件夹和资产（对于标准资产）。 此外，它还针对描述内容片段中结构化内容的自定义数据模型公开了更详细的元素。 有关详细信息，请参阅[内容片段数据模型](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments)。

### 文件夹 {#folders}

文件夹与传统文件系统中的目录类似。 文件夹只能包含资产、文件夹或文件夹和资产。 文件夹具有以下组件：

**实体**:文件夹的实体是其子元素，可以是文件夹和资产。

**属性**:

* `name` 是文件夹的名称。这与没有扩展名的URL路径中的最后一个区段相同。
* `title` 是文件夹的可选标题，可以显示该标题而不是其名称。

>[!NOTE]
>
>文件夹或资产的某些属性会映射到其他前缀。 将`jcr:title`、`jcr:description`和`jcr:language`的`jcr`前缀替换为`dc`前缀。 因此，在返回的JSON中，`dc:title`和`dc:description`分别包含`jcr:title`和`jcr:description`的值。

**LinksFolders** 公开三个链接：

* `self`:链接到自身。
* `parent`:链接到父文件夹。
* `thumbnail`:（可选）指向文件夹缩略图图像的链接。

### 资产 {#assets}

在[!DNL Experience Manager]中，资产包含以下元素：

* 资产的属性和元数据。
* 资产最初上传的二进制文件。
* 已配置多个再现。 这些图像可以是不同大小的图像、不同编码的视频或从PDF或[!DNL Adobe InDesign]文件提取的页面。
* 可选注释。

有关内容片段中元素的信息，请参阅Experience Manager资产HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[内容片段支持。

在[!DNL Experience Manager]中，文件夹包含以下组件：

* 实体：资产的子项是其演绎版。
* 属性.
* 链接.

## 可用功能{#available-features}

[!DNL Assets] HTTP API包括以下功能：

* [检索文件夹列表](#retrieve-a-folder-listing)。
* [创建文件夹](#create-a-folder)。
* [创建资产（已弃用）](#create-an-asset)
* [更新资源二进制（已弃用）](#update-asset-binary)。
* [更新资产元数据](#update-asset-metadata)。
* [创建资产演绎版](#create-an-asset-rendition)。
* [更新资产演绎版](#update-an-asset-rendition)。
* [创建资产注释](#create-an-asset-comment)。
* [复制文件夹或资产](#copy-a-folder-or-asset)。
* [移动文件夹或资产](#move-a-folder-or-asset)。
* [删除文件夹、资产或演绎版](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>为了便于读取，以下示例忽略完整的cURL注释。 此记号与[Resty](https://github.com/micha/resty)相关，后者是cURL的脚本包装器。

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## 检索列出{#retrieve-a-folder-listing}的文件夹

检索现有文件夹及其子实体（子文件夹或资源）的Siren表示形式。

**请求**:  `GET /api/assets/myFolder.json`

**响应代码**:响应代码为：

* 200 — 好 — 成功。
* 404 — 未找到 — 文件夹不存在或无法访问。
* 500 — 内部服务器错误 — 如果发生其他问题。

**响应**:返回的实体类是资产或文件夹。包含实体的属性是每个实体的全部属性集的子集。 为了获得实体的完整表示形式，客户端应检索链接所指向的URL的内容，其中`rel`为`self`。

## 创建文件夹{#create-a-folder}

创建`sling`:`OrderedFolder`。 如果提供`*`而不是节点名，则servlet将参数名用作节点名。 该请求接受以下任一条件：

* 新文件夹的Siren表示
* 一组名称 — 值对，编码为`application/www-form-urlencoded`或`multipart`/ `form`- `data`。 这对于直接从HTML表单创建文件夹很有用。

此外，文件夹的属性可以指定为URL查询参数。

如果提供的路径的父节点不存在，则API调用将失败，并带有`500`响应代码。 如果文件夹存在，调用将返回响应代码`409`。

**参数**: `name` 是文件夹名称。

**请求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**响应代码**:响应代码为：

* 201 — 创建 — 成功创建时。
* 409 — 冲突 — 如果文件夹存在。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 创建资产{#create-an-asset}

有关如何创建资产的信息，请参阅[资产上传](developer-reference-material-apis.md)。 不能使用HTTP API创建资源。

## 更新资产二进制{#update-asset-binary}

有关如何更新资产二进制文件的信息，请参阅[资产上传](developer-reference-material-apis.md)。 无法使用HTTP API更新资源二进制。

## 更新资产{#update-asset-metadata}的元数据

更新资产元数据属性。 如果更新`dc:`命名空间中的任何属性，API将更新`jcr`命名空间中的相同属性。 API不会同步两个命名空间下的属性。

**请求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**响应代码**:响应代码为：

* 200 — 确定 — 如果资产已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 创建资产演绎版{#create-an-asset-rendition}

为资产创建演绎版。 如果未提供请求参数名称，则文件名将用作格式副本名称。

**参数**:这些参数 `name` 用于格式副本的名称， `file` 并用作文件引用。

**请求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**响应代码**

* 201 — 已创建 — 如果已成功创建再现。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 更新资产演绎版{#update-an-asset-rendition}

更新会分别将资产演绎版替换为新的二进制数据。

**请求**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**响应代码**:响应代码为：

* 200 — 确定 — 如果已成功更新演绎版。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 在资产{#create-an-asset-comment}上添加评论

**参数**:参数用 `message` 于注释的消息正文和 `annotationData` JSON格式的注释数据。

**请求**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果注释已成功创建。
* 404 — 未找到 — 如果在提供的URI中找不到或访问资产，请执行以下操作。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 复制文件夹或资产{#copy-a-folder-or-asset}

复制新目标路径中可用的文件夹或资产。

**请求标头**:参数有：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite`  — 用于 `F` 防止覆盖现有目标位置的资产。

**请求**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果文件夹/资产已复制到非现有目标。
* 204 — 无内容 — 如果文件夹/资产已复制到现有目标。
* 412 - PRENIDETATION FAILED — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 移动文件夹或资产{#move-a-folder-or-asset}

将给定路径上的文件夹或资产移动到新目标。

**请求标头**:参数有：

* `X-Destination` - API解决方案作用域中要将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。使用`0`仅复制资源及其属性，而不复制其子项。
* `X-Overwrite`  — 使用强制 `T` 删除现有资源或防止覆 `F` 盖现有资源。

**请求**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**响应代码**:响应代码为：

* 201 — 已创建 — 如果文件夹/资产已复制到非现有目标。
* 204 — 无内容 — 如果文件夹/资产已复制到现有目标。
* 412 - PRENIDETATION FAILED — 如果缺少请求标头。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 删除文件夹、资产或演绎版{#delete-a-folder-asset-or-rendition}

删除提供路径上的资源(-tree)。

**请求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**响应代码**:响应代码为：

* 200 — 确定 — 如果文件夹已成功删除。
* 412 - PRENIDETATION FAILED — 如果找不到或访问根集合。
* 500 — 内部服务器错误 — 如果发生其他问题。

## 提示、最佳实践和限制{#tips-limitations}

* 在[!UICONTROL 结束时间]之后，资产及其演绎版无法通过[!DNL Assets] Web界面和HTTP API使用。 如果[!UICONTROL 开机时间]在将来，或[!UICONTROL 结束时间]在过去，则API返回404错误消息。

* 请勿使用`/adobe`作为URL或JCR路径。 请勿在此树下注册任何servlet或在JCR中创建内容。

>[!MORELIKETHIS]
>
>* [开发人员参考文档 [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

