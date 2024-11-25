---
title: 交付 API
description: 了解如何使用投放API。
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 7727aa87693cc96e3497dcda71190866b198975d
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---

# 投放API {#delivery-apis}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager资源存储库中可用的所有[批准的资源](approve-assets.md)都可以[搜索](search-assets-api.md)，然后使用投放URL传递到集成的下游应用程序。

对DAM中的已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在投放URL中。 由于为通过CDN交付资产而配置了10分钟的短生存时间(TTL)值，因此，在10分钟之内即可在所有创作和发布的界面中看到更新。

下图说明了可用的投放URL：

![投放API](assets/delivery-url.png)

下表说明了各种可用交付API的使用情况：

| 投放API | 描述 |
|---|---|
| [以请求的输出格式表示资产的Web优化二进制表示形式](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | 根据请求中发送的资产ID，以请求的输出格式返回资产的Web优化二进制表示形式。 此外，您可以定义各种图像修饰符，例如，宽度、高度、旋转、翻转、质量、裁切、格式和[智能裁切](/help/assets/dynamic-media/image-profiles.md)。 有关支持的格式和图像修饰符，请参阅[API详细信息](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat)。<br>Adobe建议对所有图像格式类型使用此API。 |
| [资产的Web优化二进制表示形式](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | 方便API，适用于响应中返回的资产的Web优化二进制表示形式。 默认格式包括标准JPEG/WEBP格式、质量=> 65和宽度=> 1024。 |
| [原始上传的资产二进制文件](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | 返回最初为资源上传的二进制文件。 Adobe建议将此API用于文档格式类型和SVG图像。 |
| [在AEM Assets创作环境中可用的资源的预生成演绎版](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | 根据请求中发送的资产ID和演绎版名称，返回在AEM Assets创作环境中可用的资产演绎版比特流。 |
| [资源元数据](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | 返回与资产关联的属性，例如标题、描述、CreateDate、ModifyDate等。 |
| 视频资源的[播放器容器](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | 返回视频资产的播放器容器。 您可以将播放器嵌入到iframeHTML元素中并播放视频。 |
| [以所选输出格式显示的播放清单](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | 以所选输出格式返回指定视频资源的播放清单文件。 您必须构建一个自定义播放器，该播放器能够通过HLS或DASH协议进行自适应流式传输，以便能够拉取播放清单文件并播放视频。 |


>[!NOTE]
>
[图像预设、智能成像和其他图像修饰符](https://adobe-aem-assets-delivery-advancemodifiers.redoc.ly/)仅作为有限可用性功能提供。 若要获得访问权限，请[创建并提交Adobe的客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。

## 投放API端点 {#delivery-apis-endpoint}

API端点因每个投放API而异。 例如，`Web-optimized binary representation of the asset in the requested output format` API的API终结点为：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

投放域的结构与Experience Manager创作环境的域类似。 唯一的区别是将术语`author`替换为`delivery`。

`pXXXX`引用项目ID

`eYYYY`引用环境ID

有关详细信息，请参阅[API详细信息](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets)。

## 投放API请求方法 {#delivery-api-request-method}

GET

## 投放API标头 {#deliver-assets-api-header}

在投放API标头中定义标头时，您需要提供以下详细信息：

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

要调用交付API，需要`Authorization`详细信息中的IMS令牌以交付受限制的资产。 IMS令牌从技术帐户中获取。 请参阅[获取AEM as a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials)以创建新的技术帐户。 请参阅[生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)以生成IMS令牌并在投放API请求标头中正确使用它。


要查看请求示例、响应示例和响应代码，请参阅[交付API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat)。
