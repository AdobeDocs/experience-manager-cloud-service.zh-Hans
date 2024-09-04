---
title: Dynamic Media 最佳实践
description: 了解在使用Dynamic Media Viewer的图像和视频以及最佳实践时Dynamic Media中的最佳实践。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '4118'
ht-degree: 0%

---

# Dynamic Media 最佳实践{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

{{work-with-dynamic-media}}

组织面临着与用户接触的渠道和设备急剧增加。 客户历程跨越实体商店、Web、移动、社交媒体、电子邮件和商务。 为了满足此需求，Adobe Experience Manager上的Dynamic Media (AEM)提供了一个全面的解决方案。 它可优化资产交付、处理个性化，并确保跨渠道和设备提供一致、高性能且品牌一致的体验。

Dynamic Media的一些关键原则包括：

* **单文件方法：**&#x200B;使用Dynamic Media，您可以存储一个主源文件，并且在交付时动态创建和优化所有大小变化和视觉效果。 此方法可节省存储成本并消除工作流的复杂性。
* **真正的全球化：**&#x200B;智能成像在内容交付期间应用，可显着减小图像大小和页面重量而不会影响视觉质量。 它针对网络带宽和设备像素比进行了优化。
* **AI支持：**&#x200B;智能裁剪是AI驱动的功能，可自动裁剪图像和视频目标点。 它消除了手动操作并高效地扩展以供企业使用。
* **轻松的视频：**&#x200B;将主源视频上传到Dynamic Media，并使用描述性音频自适应地跨多种语言流式传输它们。
* **体验查看器库：**&#x200B;自定义图像和视频的体验查看器和品牌体验查看器。 这些查看器可无缝集成到您的数字体验中。
* **新兴格式支持：** Dynamic Media允许交付3D和全景体验。

在您探索[Dynamic Media历程](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1)时，查看下面的最佳实践综合列表可以帮助您充分利用其功能。 调整这些Dynamic Media最佳实践，使其适应您的特定上下文和项目要求，以使您可跨渠道和设备优化体验。

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>随着Dynamic Media中新技术的出现，本文中的Dynamic Media最佳实践可能会随着时间的推移而不断发展。 以下信息是最新版本的Dynamic Media的最新信息。


## 将资源摄取到Dynamic Media

**业务案例：** *有效地管理大量资产，并确保只向最终用户提供相关的批准内容。*

高效地简化您对大量资产的管理。 使用Dynamic Media的&#x200B;**选择性同步**&#x200B;和&#x200B;**选择性Publish**&#x200B;功能，确保只有适当的授权内容才能到达最终用户手中。

* **选择性同步：**
一项主动功能，允许您选择要与Dynamic Media同步的资源。 例如，您可能决定仅同步那些包含已获得最终批准的资产的文件夹。 此工作流可帮助您保持对准备交付给客户的资产的控制。

* **选择性发布：**
同步资源后，通过选择性Publish ，您可以控制哪些资源对客户可见。 此功能意味着您可以管理哪些经批准的资产是通过您的渠道实际交付的，确保您的客户只能看到最佳和最相关的内容。

这两个最佳实践可帮助您更好地控制、管理和提高富媒体内容的工作效率。

想要了解更多信息？ 转到[在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)的文件夹级别配置选择性Publish。


## Dynamic Media 查看器

Dynamic Media Viewer最佳实践是旨在优化AEM上Dynamic Media资源的性能、功能和用户体验的基本准则。 这些实践可确保正确同步、发布和配置资源，以使用Dynamic Media的完整功能。

通过遵循这些最佳实践，您可以实现无缝集成、高效的资产管理和增强的查看器交互。 同步资源、使用智能裁剪以及遵守JavaScript文件包含准则都是重要实践。 这些建议有助于保持跨各种平台和设备的介质传送的完整性和可靠性。

* **同步查看器Assets：**
在使用播放器之前，请确保所有查看器资源都与Dynamic Media同步。

   * 访问位于`/libs/dam/gui/content/s7dam/samplemanager/samplemanager`的示例管理器页面。 通过此页面，您可以重新同步查看器的资产，包括现成图标、CSS文件和预设。
   * 如果您遇到任何查看器问题，请转到[Dynamic Media查看器疑难解答](/help/assets/dynamic-media/troubleshoot-dm.md#viewers)文章。

* **Publish Assets：**
在投放查看器中查看资产之前，请确保已发布资产。
* **自动播放视频已静音：**
对于视频中的自动播放功能，请使用静音视频设置，因为浏览器会限制按音量播放视频。
* **智能裁剪：**
使用用于智能裁剪的图像v3组件增强图像资产呈现。
* **JavaScript文件包含：**
页面上仅包含主查看器JavaScript文件。 避免引用查看器的运行时逻辑可能下载的其他JavaScript文件。 具体而言，请勿从`/s7viewers`上下文HTML（称为整合SDK包含）直接链接到Consolidated SDK `Utils.js`库。 查看器的逻辑管理`Utils.js`或类似的运行时查看器库的位置，这些库可以在版本之间更改。 Adobe不会保留服务器上包含的旧版本辅助查看器，因此直接引用这些版本可能会破坏查看器在将来更新中的功能。
* **嵌入准则：**
使用文档嵌入特定于每个查看器的准则。
想要了解更多信息？ 转到AEM Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers)的[查看器。
* **SDK教程和示例：**
查看[Viewer SDK教程](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/c-tutorial)和[HTML5 SDK应用程序示例](https://s7d9.scene7.com/s7sdk/2024.5/docs/jsdoc/index.html)，以全面了解SDK组件API。


## 准备资产以进行交付

### 组织您的资源

**业务案例：** *有效地组织资源以简化工作流。*

要获得可简化工作流的高效资产组织，请使用以下一个或多个最佳实践：

* **在文件夹中组织资源：**
有效地组织资产包括将资产分类到文件夹中，类似于计算机上的文件组织。 正确的命名、结构化子文件夹以及这些文件夹中的文件管理对于高效的资产处理至关重要。 实施系统化的命名惯例和元数据惯例可最大限度地提高数字资产存储库的效用。
想要了解更多信息？ 转到[整理文件夹](/help/assets/organize-assets.md#organize-using-folders)中的资源。
* **使用标记组织资源：**
为资产添加标记可增强搜索性、收藏集创建和搜索排名。 Adobe Sensei的人工智能采用自学习算法来进行精确标记，从而实现快速资源检索。 Adobe Sensei还可以识别相关标记（包括自定义标记）并将它们分配给资产，通过自动的描述性标记来简化资产管理。
想要了解更多信息？ 转到[使用标记](/help/assets/organize-assets.md#use-tags-to-organize-assets)整理资源。
* **将资源组织为收藏集：**
Dynamic Media与Experience Manager Assets一起支持在用户之间高效地创建、编辑和共享资源集合。 您可以建立各种收藏集类型，包括静态列表和基于搜索的动态编译。 这些收藏集类型可通过可自定义的访问和编辑权限在多个位置共享。
想要了解更多信息？ 转到[将资源组织为收藏集](/help/assets/manage-collections.md)。
* **使用配置文件组织资源：**
处理配置文件可自动执行指定文件夹中的资产处理，从而简化组织。 随着数字资产收藏集的扩展，通过标准化元数据、文件名和文件夹结构，可以一致而准确地应用这些配置文件。
想要了解更多信息？ 转到[使用个人资料整理资源](/help/assets/organize-assets.md#organize-to-use-profiles)。



### 优化图像质量

**商业论证：** *从Dynamic Media获取高质量的图像。*

提高图像质量需要仔细考虑各种因素。 这可能是一个非常耗时的过程。 但是，有一些行之有效的实践可以帮助您获得理想的结果。 其中一些最佳实践包括如何获得最佳图像大小、图像锐化以及要使用的最佳图像格式。

想要了解更多信息？ 转到[优化图像质量的最佳实践](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)。

由于对图像质量的感知因人而异，因此有时系统地进行实验对于获得理想结果至关重要。 Adobe Experience Manager通过100多条Dynamic Media命令来增强图像，从而帮助实现了这个过程。

想要了解更多信息？ 观看[Dynamic Media快照](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)（3分钟17秒）。

要评估这些命令对图像质量的影响，您可以将图像上传到Dynamic Media，使用工具在指定URL处的界面，并应用要尝试的命令。

想试试吗？ 启动[Dynamic Media快照](https://snapshot.scene7.com/)

### 对应用于图像的样式进行标准化

**业务案例：** *有效地标准化应用于我的图像资产的样式和转换。*

在Dynamic Media中定期使用图像预设，以便您可以一致且动态地调整图像大小、格式和属性。 将图像预设视为宏：它是一组指定的用于调整大小和设置格式的命令。 例如，如果您的网站需要各种大小和格式的产品图像，并对桌面和移动设备进行特定压缩，则图像预设会高效地自动完成此过程。

想试试吗？ 转到[创建图像预设的基础知识以渲染资产](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### 调整图像和视频的焦点和帧设置

**业务案例：** *确保我的图像或视频的主要兴趣点跨设备保持焦点。*

智能裁剪是Dynamic Media中的一项功能，它使用Adobe的AI和机器学习框架Adobe Sensei来自动裁剪图像和视频。 它智能地检测并关注图像或视频中的主要主题或兴趣点。 这种智能功能可确保焦点在台式计算机和移动设备上的各种屏幕尺寸中得以保持。

最佳做法是使用智能裁剪创建图像配置文件。 在配置文件中，您可以定义各种屏幕大小并让Adobe Sensei完成其余步骤，以确保您的图像和视频始终针对查看者的设备而优化。

想要了解更多信息？ 观看[在AEM Assets Dynamic Media中使用智能裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)（6分钟35秒）和[在视频中使用Dynamic Media智能裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video)（6分钟22秒）。

### 改进SEO排名

**业务案例：** *配置Dynamic Media以获得改进的SEO排名。*

请定期使用以下建议，以确保您的图像能够有效地帮助您制定整体SEO策略。

* **有意义的图像文件名：**
使用反映图像内容的描述性文件名。 例如，

   * 使用 `myCompany-Silver-Wrist-Watch`
   * *避免* `myCompany_Silver_Wrist_Watch`或`myCompanySilverWristWatch`

  这样做有助于搜索引擎了解图像上下文并改进SEO。 Google在文件名中首选使用连字符，而不是下划线或空格。 此外，请避免在文件名中连接单词。
* **自定义域：**
实施包含您的公司或品牌名称的自定义域，以增强品牌认知度和信任。 例如，

   * 使用 `http://images.mycompany.com/is/image/companyname/`
   * *避免* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`

* **SEO友好的文件夹结构：**
以包含公司名称或品牌的文件夹结构组织图像，以便更好地编制索引，如`http://images.mycompany.com/is/image/companyname/`。
* **Dynamic Media规则集：**
了解如何根据各种因素有条件地转换URL，从而增强SEO和用户体验。
想要了解更多信息？ 转到[使用规则集转换URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)。
* **智能成像和智能裁切：**
使用Dynamic Media中的智能成像和智能裁切功能来提供优化且响应式图像。 这样做不仅会缩短页面加载时间，还会对SEO排名产生积极影响。
想要了解更多信息？ 转到[智能成像](/help/assets/dynamic-media/imaging-faq.md)，或观看[在AEM Assets Dynamic Media中使用智能裁切](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)（6分钟35秒）。

请记住，这些最佳实践与Google的图像SEO最佳实践高度一致。 此类实践强调通过适当的命名约定、结构化数据和优化的图像交付为搜索引擎提供上下文和清晰度的重要性。

想要了解更多信息？ 转到[Google的URL结构最佳实践](https://developers.google.com/search/docs/crawling-indexing/url-structure)和[Google图像SEO最佳实践](https://developers.google.com/search/docs/appearance/google-images)

### 使用命令动态增强图像并创建视觉效果

**商业案例：** *将丰富的视觉效果应用于图像。*

Dynamic Media提供了一套用于增强图像和动态创建视觉效果的命令，而无需多个静态资源。 下面简要说明了其中一些流程，并提供了一些可指导您的示例：

#### 源图像内的效果

| 任务 | 要做什么 |
| --- | --- |
| **上载并发布原始图像** | ·首先，将原始图像上传到Dynamic Media。<br>·确保已发布并通过URL访问。<br>·在此示例中，具有白色背景的手表的库存图像（我们将其称为“图像X”）上传到Dynamic Media。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer) |
| **创建掩码** | ·开发定义主题（要应用效果的区域）和背景（要更改的区域）的蒙版。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)<br>·蒙版通常是灰度图像，其中白色代表主题，黑色代表背景。 您可以使用Adobe Photoshop等工具创建蒙版。<br>想了解更多信息？ 转到[在Photoshop](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html)中创建和编辑快速蒙版。<br>·对于“图像X”，请创建一个精确概述要增强的主题的蒙版。 例如，人员、对象等。 |
| **应用Dynamic Media URL命令以获得效果** | 在蒙版完成后，使用URL命令应用阴影等效果，或将背景颜色更改为“图像X”。 以下是两个示例：<br><br> · **阴影效果：**<br>&#x200B;若要沿着主题边界添加阴影效果，请编辑URL，如下所示：<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25)<br>在此URL中，`$shadow$`参数将创建阴影效果，`color=0,0,0`将阴影颜色设置为黑色。<br>· **背景颜色更改：**<br>&#x200B;要更改背景颜色，请使用具有不同背景颜色值的URL：<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0)<br>在此示例中，`color=255,255,0`将背景颜色设置为黄色。 将背景编辑为特定颜色以实现视觉效果。 |

#### 添加图像边框

Dynamic Media允许您直接通过URL处理图像，使其成为创建动态数字体验的强大工具。 以下是一些示例。 让我们从以下原始图像URL开始： [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel)。

| 任务 | 要做什么 |
| --- | --- |
| **白色边框** | 要添加白边框，请使用以下URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10)<br>在此URL中，`extend=10,10,10,10`参数指定所有边框10像素的边框大小。 |
| 沿白色边框&#x200B;**模糊** | 若要沿白色边框添加模糊效果，您可以按如下方式编辑URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0)<br>在此URL中，`effect=-1`参数应用模糊效果，而`op_blur=60`控制模糊强度。 |
| **沿外部边界的投影效果** | 若要沿外部边界添加阴影效果，请使用此URL：<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0)<br>参数`$shadow$`创建阴影效果，并且`color=0,0,0`将阴影颜色设置为黑色。 |

欢迎尝试使用这些URL来实现所需的视觉效果。

#### 创建图像叠加

如果您希望在现有图像上叠加徽标或图标，Dynamic Media提供了一种简单的方法使用URL命令来实现这一点。 我们来分几步吧。

| 步骤 | 要做什么 |
| --- | --- |
| **上载并发布基本映像** | 首先，上载并发布要在其上叠加徽标或图标的基本图像。 您可以使用任何图像作为基础。<br>例如，以下是基本映像：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)。 |
| **上载并发布徽标或图标图像** | 接下来，上传并发布要叠加在基本图像上的图像。 此图像应是透明的PNG，其中应包含要叠加的徽标或图标。<br>下面是即将叠加的具有透明效果的星形对象的透明PNG图像：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **应用Dynamic Media URL** | 现在，创建一个Dynamic Media URL，以组合基本图像和徽标或图标图像。 可以使用URL命令达到此效果。<br>URL结构类似于：<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png)<br>其中资产<br>· `hotspotRetailBaseImage`是基本图像。<br>· `starxp`是徽标/图标图像。<br>· `layer=1`指定徽标或图标应叠加在基本图像上。<br>· `scale=1.25`调整徽标/图标的大小。<br>· `posN=0.33,-.25`确定徽标/图标相对于基本图像的位置。<br>· `fmt=png`确保输出为PNG格式。 |

了解更多信息？ 请转到[src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src)以了解有关`src`命令和其他Dynamic Media URL命令的更多详细信息。


#### 覆盖促销文本

以下是使用HTML和CSS在图像上叠加促销文本消息的步骤。

| 步骤 | 要做什么 |
| --- | --- |
| **上载并发布基本映像** | 首先，上载并发布要在其上叠加文本的基本图像。 您可以使用任何喜欢的图像。 例如，以下是示例基本图像：<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **应用Dynamic Media文本运算符** | 使用Dynamic Media，您可以应用文本运算符以将动态文本直接叠加到图像上。 以下示例URL演示了此功能：<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial；%7d%7d%7b\colortbl+\red255\green255\blue255；%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial；%7d%7d%7b\colortbl+\red255\green255\blue255；%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600) |

#### 调整大小并裁切各种用例

##### 图像大小调整基础知识

图像大小调整涉及改变图像的尺寸、分辨率和文件大小。 以下是需要考虑的一些要点：

* **像素合成：**
数字图像由称为像素的小点组成。 创建图像时，图像具有特定数量的像素。 调整大小涉及添加或减去像素以更改图像的尺寸、分辨率和文件大小。
* **宽高比：**
保持纵横比（宽度和高度的关系）对于防止扭曲至关重要。 无论您是要使图像变大（放大）还是变小（缩小），保留纵横比均可确保视觉一致性。
* **质量注意事项：**
调整大小可能会影响图像质量。 避免急剧放大，因为它可能会导致像素化。 相反，请考虑以更大的大小和分辨率再现图像。 对于较小的图像，请使用适当的工具来保持分辨率。

##### 裁切与调整大小

裁切和调整大小是Dynamic Media中的技术，这些技术允许您变换图像以适合各种用例，无论是在创建缩略图、产品显示图像还是横幅。

* **裁切：**
涉及移除部分图像以改变其构成和框架。 它不会更改总体维度，但侧重于特定区域。
* **正在调整大小：**
调整整个图像的尺寸、分辨率和文件大小，同时保持宽高比。

让我们探讨一个涉及以下起居室图像的用例：

* **原始客厅图像：**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **缩略图（200像素x 200像素）：**
适合快速加载或显示的较小版本。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop)
* **带有裁切的缩略图（200像素x 200像素）：**
裁剪以专注于沙发区域。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **产品显示图像（800像素x 600像素）：**
为了展示沙发而裁切和调整大小。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **横幅(1720 px x 820 px)：**
从原始图像派生，强调房间。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop)

您可以随意探索这些变体，以满足您的特定需求。
想要了解有关URL中可用命令的更多信息？ 转到[命令引用](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference)。

### 投放GIF图像

**商业案例：** *使用Dynamic Media的流GIF*

您可以通过Dynamic Media上传和投放GIF。 要渲染动画GIF，请在URL中将`is/image`替换为`is/content`。 例如，如果您已上传`abc.gif`，请使用以下内容：

* 此URL路径呈现GIF的静态视图：

  ```
  https://your.domain.com/is/image/yourfolder/abc
  ```

* 此URL路径将渲染GIF的动画视图：

  ```
  https://your.domain.com/is/content/yourfolder/abc
  ```

>[!NOTE]
>
>在URL路径中使用`is/content`时，图像转换命令未应用于资源。

### Publish我的网站视频

**商业案例：** *快速发布营销网站的视频。*

* **选择视频配置文件：**
首先，在Dynamic Media中，您应该选择合适的视频配置文件。 您可以在视频配置文件下选择在AEM Assets中可用的*自适应视频编码*&#x200B;配置文件。 这些预定义的编码设置可确保您的视频在各种设备和带宽条件下均能优化播放。 或者，您也可以创建自己的自适应视频配置文件。
* **分配配置文件：**
将所选视频配置文件分配给要将视频上传到的文件夹。 此步骤可确保在上传过程中应用正确的编码设置。
* **上传原始视频：**
上传原始视频文件。 确保它是一个高分辨率的高质量视频。 源视频越好，最终结果越好。
* **预览和发布：**
预览视频，以便确保一切按预期显示。 满意后，即可发布它。 此步骤使受众能够访问视频。
* **链接或嵌入：**
发布后，您有两个选项。

   * **直接链接：**
使用提供的URL直接链接到视频。 在营销网站上以适当的方式超链接它。
   * **嵌入视频：**
复制提供的嵌入代码并将其粘贴到您希望视频显示的网页HTML中。 这样，视频就可以直接在您的网站上播放。

想要了解更多信息？ 转到[视频](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video)。

### 配置视频以获得最佳质量和参与

**商业论证：***设置视频以获得最佳质量和参与度。*

要确保视频的最佳质量和参与度，请考虑实施以下最佳实践策略的组合：

* **使用内置HTML5视频查看器：**
Dynamic MediaHTML5视频查看器预设是可靠的视频播放器。 使用它们可避免与HTML5视频播放和移动设备相关的常见问题。
这些预设可解决自适应比特率流交付和桌面浏览器访问受限等挑战。
想要了解更多信息？ 转到[最佳实践：使用HTML5视频查看器](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer)。

* **使用Dynamic Media视频配置文件：**
Dynamic Media中的视频配置文件可帮助实现高效的视频管理、一致的品质和自适应流式传输。
想要了解更多信息？ 转到[Dynamic Media视频配置文件](/help/assets/dynamic-media/video-profiles.md)。

* **遵循视频编码的最佳实践：**
应用视频编码配置文件，在编码期间保持原始视频质量而不过度缩放。
想要了解更多信息？ 转到[视频编码最佳实践](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos)。

* **采用自适应流式传输而不是渐进式流式传输：**
自适应流根据观看者的Internet连接速度和设备功能调整视频质量。
它使用HLS （HTTP实时流）或DASH (`Dynamic Adaptive Streaming over HTTP`)之类的协议来确保最佳播放质量。
与线性交付视频的渐进式流不同，自适应流可最大程度地减少缓冲并提供无缝观看体验。

* **在您的帐户上启用DASH （通过HTTP进行数字自适应流式传输）：**
DASH通过自适应流的方式动态地提供视频内容。
要启用DASH，请为您的环境创建支持工单。
想要了解更多信息？ 转到[在你的Dynamic Media帐户上启用DASH](/help/assets/dynamic-media/video.md#enable-dash)。

### 将视频国际化，以便使用多语言

**业务案例：** *使视频准备好供多语言使用。*

多语言消费视频的国际化对于触及全球受众至关重要。 Dynamic Media提供了一些功能来帮助您实现这一目标。

* **上传您的视频：**
   * 首先，创建视频编码配置文件。 您可以使用Dynamic Media附带的预定义自适应视频编码配置文件或创建自己的自定义配置文件。
   * 将视频处理配置文件与您上传主源视频的一个或多个文件夹关联。
   * 将您的主源视频上传到这些文件夹。 Dynamic Media会根据分配的视频处理配置文件对它们进行编码。
   * Dynamic Media主要支持最小分辨率大于25×25的短格式视频（最长为30分钟）。 每个视频文件最多可以上传15 GB1。

* **管理您的视频：**
   * 在AEM中整理、浏览和搜索视频资源。
   * 预览和发布视频资源。
   * 查看源视频及其编码的呈现版本以及关联的缩略图。
   * 编辑视频属性，如标题、描述和标记2。

* **本地化：**
   * 对于每个目标地理/语言，创建音频轨道和字幕。
   * 从AEM界面将这些音频和字幕轨道添加到您的视频中。
   * 用户播放视频时，可以选择音频和字幕的首选语言。

* **正在发布：**
   * 如果您将AEM用作Web内容管理(WCM)系统，则可以直接将视频添加到网页。
   * 如果您使用的是第三方WCM系统，则可以使用URL或嵌入代码在网页上链接或嵌入视频。

想要了解更多信息？ 转到[关于Dynamic Media中对视频的多个字幕和音轨支持](/help/assets/dynamic-media/video.md#about-msma)或观看[向视频添加多个字幕和音轨](https://delivery-p106302-e1008131.adobeaemcloud.com/adobe/assets/urn:aaid:aem:daf9a222-9f7f-4333-b167-98cb4c63a1f8/play)（1分钟41秒）。


## 将资产交付给客户

### 优化图像大小并缩短页面加载时间

**业务案例：** *优化任何浏览器或屏幕的图像大小并减少页面加载时间。*

Dynamic Media智能成像是一款功能强大的工具，通过基于客户端的浏览器功能自动优化图像的格式、大小和质量，来增强图像投放性能。

Adobe建议您使用智能成像的功能，而不是手动将图像格式设置为`webp`或`avif`。 原因如下：

* **浏览器兼容性：**
智能成像可确保交付的图像格式与用户的浏览器兼容。
* **最佳压缩：**
它根据特定的浏览器、网络条件和屏幕分辨率来选择最佳的压缩格式。
* **新式格式：**
虽然`avif`是一种较新的格式，提供了更好的压缩，但并非所有浏览器都支持它。
* **最佳实践：**
为确保获得最佳的Web优化格式，您可以信任智能成像进行格式选择，而不是使用命令`fmt=webp`或`fmt=avif`手动进行格式选择。

通过依赖智能成像，您可以确保以尽可能高效的方式提供图像，并根据每个用户的浏览环境量身定制。 此方法简化了流程，并且可以在图像加载时间和整体用户体验方面提高性能。

想要了解更多信息？ 转到[智能成像](/help/assets/dynamic-media/imaging-faq.md)。

### 将资产过帐交付给客户

**业务案例：** *发布新内容或覆盖现有内容后，如何确保更改立即显示在CDN上？*

CDN（内容分发网络）缓存Dynamic Media资产，以快速将其交付给客户。 更新这些资源后，所做的更改必须立即在网站上生效。 通过清除或使CDN缓存失效，Dynamic Media交付的资源可以快速更新。 此方法无需根据TTL（生存时间）值（通常设置为10小时）等待缓存过期。 根据您的特定用例，您可以相应地更新CDN TTL（生存时间）设置。

想要了解更多信息？ 转到[通过Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)使CDN缓存失效。
