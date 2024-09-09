---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 将资源选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 3%

---

# Dynamic Media与OpenAPI功能集成 {#integrate-asset-selector-dynamic-media-open-apis}

Asset Selector允许您使用各种Adobe应用程序进行集成，以使它们能够无缝地协同工作。


## 先决条件 {#prereqs-polaris}

如果要将资产选择器与Dynamic Media以及OpenAPI功能集成，请使用以下先决条件：

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* 要访问具有OpenAPI功能的Dynamic Media，您必须具有以下功能的许可证：
   * Assets存储库(例如，Experience Manager Assetsas a Cloud Service)。
   * AEM Dynamic Media。
* 只有[个批准的资产](/help/assets/approve-assets.md)可用于确保品牌一致性。

## Dynamic Media与OpenAPI功能集成 {#adobe-app-integration-polaris}

资产选择器与Dynamic Media OpenAPI进程的集成涉及各种步骤，包括创建自定义的Dynamic Media URL或准备选择Dynamic Media URL等。

### 将Dynamic Media的资源选择器与OpenAPI功能集成 {#integrate-dynamic-media}

`rootPath`和`path`属性不应包含在具有OpenAPI功能的Dynamic Media中。 相反，您可以配置`aemTierType`属性。 以下是配置的语法：

```
aemTierType:[1: "delivery"]
```

利用此配置，可查看所有批准的资产，但不包含文件夹或采用平面结构。 有关详细信息，请导航到[资产选择器属性](/help/assets/asset-selector-properties.md)下的`aemTierType`属性。


### 从批准的资产创建动态投放URL {#create-dynamic-media-url}

设置资源选择器后，将使用对象架构从所选资源创建动态投放URL。
例如，在选择资产时接收的来自对象数组中的某个对象的模式：

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

所有选定资源均由用作JSON对象的`handleSelection`函数承载。 例如，`JsonObj`。动态投放URL是通过组合以下运营商创建的：

| 对象 | JSON |
|---|---|
| 主机 | `assetJsonObj["repo:repositoryId"]` |
| API根 | `/adobe/dynamicmedia/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| 格式 | `.jpg` |

#### 批准的资产交付API规范 {#approved-assets-delivery-api-specification}

URL格式：
`https://<delivery-api-host>/adobe/dynamicmedia/deliver/<asset-id>/<seo-name>.<format>?<image-modification-query-parameters>`

其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* API根是`"/adobe/dynamicmedia/deliver"`
* `<asset-id>`是资产标识符
* `<seo-name>`是资源的名称
* `<format>`为输出格式
* `<image modification query parameters>`作为已批准资产的投放API规范的支持

#### 批准的资产交付API {#approved-assets-delivery-api}

动态投放URL具有以下语法：
`https://<delivery-api-host>/adobe/assets/deliver/<asset-id>/<seo-name>`，其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* 原始节目投放的API根为`"/adobe/assets/deliver"`
* `<asset-id>`是资产标识符
* `<seo-name>`是包含扩展名或不包含扩展名的资源的名称

### 准备挑选动态投放URL {#ready-to-pick-dynamic-delivery-url}

所有选定资源均由用作JSON对象的`handleSelection`函数承载。 例如，`JsonObj`。动态投放URL是通过组合以下运营商创建的：

| 对象 | JSON |
|---|---|
| 主机 | `assetJsonObj["repo:repositoryId"]` |
| API根 | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

以下是遍历JSON对象的两种方式：

![动态投放URL](assets/dynamic-delivery-url.png)

* **缩略图：**缩略图可以是图像，资产可以是PDF、视频、图像等。 但是，您可以将资产缩略图的高度和宽度属性用作动态投放演绎版。
以下演绎版集可用于PDF类型资源：
在sidekick中选择PDF后，选择上下文会提供以下信息。 以下是遍历JSON对象的方式：

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

在上面的屏幕快照中，如果需要PDF，则需要将PDF原始演绎版的投放URL合并到目标体验中，而不是合并其缩略图。 例如，`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf?accept-experimental=1`

* **视频：**您可以为使用嵌入式iFrame的视频类型资源使用视频播放器URL。 您可以在Target体验中使用以下数组演绎版：
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  上述屏幕快照中的代码片段是视频资源的一个示例。 它包括呈现版本链接数组。 摘录中的`selection[5]`是图像缩略图的示例，可用作目标体验中视频缩略图的占位符。 演绎版数组中的`selection[5]`适用于视频播放器。 这提供了一个HTML，可以设置为iframe的`src`。 它支持自适应比特率流，该流是Web优化的视频交付。

  在上例中，视频播放器URL为`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play?accept-experimental=1`

### 配置自定义筛选条件 {#configure-custom-filters-dynamic-media-open-api}

通过OpenAPI功能的Dynamic Media资源选择器，可配置自定义属性以及基于这些属性的过滤器。 `filterSchema`属性用于配置此类属性。 自定义项可以作为`metadata.<metadata bucket>.<property name>.`公开，可以根据它配置筛选器，其中，

* `metadata`是资产的信息
* `embedded`是用于配置的静态参数，并且
* `<propertyname>`是您配置的筛选器名称

对于配置，对于要配置的筛选器，在`jcr:content/metadata/`级别定义的属性将公开为`metadata.<metadata bucket>.<property name>.`。

例如，在用于具有OpenAPI功能的Dynamic Media的资源选择器中，`asset jcr:content/metadata/client_name:market`上的某个属性被转换为`metadata.embedded.client_name:market`以进行筛选器配置。

要获取名称，必须完成一次性活动。 对资产进行搜索API调用，然后获取属性名称（本质上是存储桶）。

### 具有OpenAPI功能的Dynamic Media的资源选择器用户界面 {#interface-dynamic-media-open-api}

在与Adobe的微前端资源选择器集成后，您可以在Experience Manager资源存储库中查看所有已批准资源的仅资源结构。

具有OpenAPI功能UI的![Dynamic Media](assets/polaris-ui.png)

* **A**：[隐藏/显示面板](#hide-show-panel)
* **B**： [Assets](#repository)
* **C**： [排序](#sorting)
* **D**：[过滤器](#filters)
* **E**：[搜索栏](#search-bar)
* **F**： [按升序或降序排序](#sorting)
* **G**：取消选择
* **H**：选择单个或多个资源

>[!MORELIKETHIS]
>
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
