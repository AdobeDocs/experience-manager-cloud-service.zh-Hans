---
title: 使用具有OpenAPI功能的Dynamic Media优化图像
description: 了解如何使用具有OpenAPI功能的Dynamic Media的图像优化功能，在公共交付之前快速优化图像
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 5a01aff1d6c10d86e2faef22da2dbe724e24e673
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# 使用具有OpenAPI功能的Dynamic Media优化图像{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]提供图像优化功能，如[!DNL Smart Crop]、[!DNL Image Presets]和[!DNL Smart Imaging]。 这些功能有助于提供高质量、响应迅速的图像，这些图像可以跨不同的设备和网络快速加载。

## 智能裁切{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[智能裁切](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)是[!DNL Dynamic Media with OpenAPI capabilities]的动态大小调整功能。 [!DNL Smart Crop]是一种高级图像处理技术，它使用AI支持的内容感知裁剪来智能地裁剪各种屏幕大小的图像，同时保留裁剪版本中的可视上下文。 人工智能分析图像以识别焦点或目标点，然后自动裁剪图像以在所有裁剪的版本中保留焦点。 [!DNL Smart Crop]是响应式设计的一个关键元素，它提供了一种经济高效且省时的方法来裁剪图像。

请参阅[Dynamic Media图像配置文件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles)文章以了解如何在[中](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles)创建智能裁剪演绎版[!DNL Admin View]、[将它们应用于文件夹](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders)或[编辑演绎版](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image)这些演绎版已应用于图像或文件夹。 在此[!DNL Smart Crop]视频[中了解如何分步创建](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)。

[!DNL Smart Crop]参数需要named-smartcrop-profiles存在并已应用于资源。 请参阅[智能裁剪配置文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request)，了解有关[!DNL Smart Crop]参数以及如何应用名为[!DNL Smart Crop]的配置文件的更多信息。

>[!IMPORTANT]
>
> 您只能在“管理员”视图中创建[!DNL Smart Crop]呈现。

## 图像预设{#image-presets-using-dynamic-media-with-openapi-capabilities}

在[中使用](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request)图像预设[!DNL Dynamic Media with OpenAPI capabilities]功能即时转换图像。 [!DNL image preset]是输出图像的预定义大小调整和格式规则集。

[!DNL Dynamic Media with OpenAPI capabilities]使用预设名称即时转换图像并即时生成其演绎版。 当您通过包含预设参数的[!DNL Dynamic Media with OpenAPI]投放URL请求图像时，[!DNL DM with OpenAPI]应用预设的转换，根据需要创建演绎版，并将其交付给用户。

您可以通过图像的[!DNL Dynamic Media with OpenAPI]投放URL将单个预设应用于多个图像。 这可以确保跨资源的一致格式，而无需手动编辑每个资源。

请参阅[管理图像预设](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets)文章以了解[如何在管理员视图中创建图像预设](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets)，以及[如何创建响应式图像预设](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset)，这些预设可自动调整资产以适合不同的屏幕大小。

### 使用图像预设的好处{#benefits-of-image-presets}

[!DNL Image Presets]为在[!DNL Dynamic Media with OpenAPI]中管理和投放图像提供了几个优势。 一些主要优势包括：

* 预设可缩短图像交付URL。 请使用单个预设，而不是添加多个使投放URL更长的图像修饰符。 较短的URL更容易管理，并确保跨网站、移动应用程序、电子邮件和其他渠道的一致图像交付。
* 图像预设从源图像文件创建即时演绎版。 这种按需格式副本生成功能消除了创建和存储同一文件的多个静态格式副本的需要，从而节省了时间和存储。
* 一次将单个预设应用于大量资产，避免分别手动编辑每个资产，确保一致的格式并启用可扩展性。
* 更新预设的参数时，使用该预设的所有图像都会自动重新格式化。 这通过集中格式更新简化了编辑，无需重新编辑单个资产或Web代码。
* 利用CDN缓存的动态呈现来提高效率和性能，从而加快加载速度并优化跨设备和网络的性能。

### 使用图像预设{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

创建[!DNL Image Presets]后，您可以将其用于以下工作流：

* [在图像交付URL中使用预设动态创建其演绎版，然后再将其交付给最终用户](#use-presets-in-delivery-urls)
* [在AEM Sites中进行创作时使用预设](#use-presets-during-authoring-in-aem-sites)

#### 在图像投放URL中使用预设{#use-presets-in-delivery-urls}

预设使您的投放URL更短且更易于使用。  每个预设名称用作投放URL中的唯一标识符。 请引用预设名称以立即生成其演绎版，而不是向资产的投放URL添加多个修饰符。 [了解如何将Dynamic Media图像预设应用于图像](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets)。
以下示例将带有预设的URL与没有预设的URL进行比较。

**没有预设的URL （长URL）**：

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true
```

带有预设的&#x200B;**URL （短URL）**：

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail
```

预设缩略图捆绑了相同的图像修饰符设置。

#### 在AEM Sites中进行创作时使用预设{#use-presets-during-authoring-in-aem-sites}

启用[!DNL Image Presets]支持后，作者可以在[!DNL AEM Sites]创作页面中的页面编辑期间选择[!DNL Dynamic Media]。

执行以下步骤以在创作页面中使用图像预设：

1. 导航到站点创作页面。
1. 执行[访问AEM页面编辑器中的远程资源](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor)部分中的步骤，以使用[!DNL Asset Selector]面板选择资源。
1. 在[!DNL asset selector]面板中，向下滚动到&#x200B;**[!UICONTROL 预设类型]**，并在`Preset=Preset Name`图像修饰符&#x200B;**[!UICONTROL 字段中指定]**。

   ![预设](/help/assets/assets/preset-in-asset-selector-panel.png)

## 智能图像处理{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

当您使用[!DNL Dynamic Media with OpenAPI capabilities]进行图像投放时，将通过[智能成像](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/)自动优化图像。 优化的投放确保图像加载更快，具有最大的视觉质量和最小的文件大小。 这样可以在各种设备和网络中实现最快的页面加载速度并始终保持较高的视觉质量，同时占用最少的带宽，从而使您的网站速度更快、响应速度更快。

[!DNL Smart Imaging]包括以下功能：

* [自动格式转换](#auto-format-conversion)
* [网络带宽优化](#network-bandwidth-optimisation)

### 自动格式转换{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [自动将图像转换为现代的Web优化格式，如AVIF或WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request)。 转换取决于浏览器的功能和[license-entitlement](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)，而不管请求的格式如何。

AVIF和WEBP格式提供了更好的压缩，使图像变得更小，交付和加载速度更快。 AVIF用作默认格式，因为它处理所有浏览器功能。

[!DNL Dynamic Media with OpenAPI]使用`auto-format`查询参数来控制浏览器将图像转换为各种格式以进行优化投放的行为。 自动格式转换包括&#x200B;**自动提升**&#x200B;和&#x200B;**自动降级**。 当系统通过JPEG或PNG促销网络优化格式（AVIF或WEBP）以进行交付时，它称为自动促销。

默认情况下，`auto-format`查询参数设置为`true`。 启用`auto-format` (true)时，系统会忽略请求的格式，并根据图像特征、浏览器功能和[许可证授权](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate)自动选择Web优化格式（AVIF或WEBP）。

当`auto-format`为true时，系统按以下顺序提供图像格式：

* ***AVIF***：如果浏览器支持并且许可证允许，将交付AVIF。 这称为自动促销活动。
* ***WEBP***：如果AVIF不受支持或未经许可，则会交付WEBP。 这也是自动促销活动。
* ***JPEG***：仅当不支持AVIF和WEBP时，才会交付JPEG，并且图像没有Alpha通道（透明度）。 这称为自动降级。
* ***PNG***：当浏览器不支持新式格式并且图像具有Alpha通道（透明度）时，将传递PNG。 这也称为自动降级。

通过将查询参数设置为`auto-format`来禁用`false`，然后指定所需的格式以获取以该格式传送的图像。

### 网络带宽优化{#network-bandwidth-optimisation}

图像会根据客户机的网络状况自动优化，以确保更快的交付和平顺的加载。 [Quality](#quality-parameter)和[Max-quality](#max-quality-parameter)参数通过控制图像压缩级别自动调整质量，其值介于1到100之间。

查看`quality`和`max-quality `参数的以下关键行为：

* 如果同时指定了[!DNL quality]和[!DNL max-quality]，则[!DNL quality]优先。
* 如果仅指定[!DNL quality]，则无论加载时间如何，都会根据网络速度传递质量。
* 如果仅指定[!DNL max-quality]，则图像质量将根据网络状况自动调整，提供最佳质量，最高可达指定的[!DNL max-quality]值。
* 如果两者均未指定，则系统将使用默认值`max-quality`应用动态优化`85`。

#### 质量参数{#quality-parameter}

品质参数将图像质量优先于加载速度。 它将输出图像质量固定到请求的值（介于1和100之间）并忽略网络条件。 了解有关[质量参数](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)的更多信息。

#### Max-quality参数{#max-quality-parameter}

Max-quality可根据客户的网络速度平衡图像质量和加载时间。 它通过降低较慢网络上的图像质量来优先处理较快的加载时间，同时仍提供给定网络条件下的最高质量(1-100)。 了解有关[max-quality参数](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request)的更多信息。
