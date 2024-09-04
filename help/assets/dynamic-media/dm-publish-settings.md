---
title: 为图像服务器配置Dynamic Media Publish设置
description: 了解如何为图像服务器配置Dynamic Media Publish设置，其中涵盖颜色管理、安全性和缩略图图像等。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: b0891095-e4a9-4dd5-8dfd-a576bc47d082
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '3333'
ht-degree: 0%

---

# 为图像服务器配置Dynamic Media Publish设置

<!-- hide: yes
hidefromtoc: yes -->

{{work-with-dynamic-media}}

配置Dynamic Media Publish安装程序仅在以下情况下可用：

* 您在Adobe Experience Manager as a Cloud Service中具有&#x200B;*现有* **[!UICONTROL Dynamic Media配置]** (在&#x200B;**[!UICONTROL Cloud Service]**&#x200B;中)。 请参阅[在Cloud Service中创建Dynamic Media配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
* 您是具有管理员权限的Experience Manager系统管理员。

Dynamic Media Publish安装程序旨在供有经验的网站开发人员和程序员使用。 AdobeDynamic Media建议更改这些发布设置的用户熟悉AdobeDynamic Media、HTTP协议标准和惯例，以及基础映像技术。

“Dynamic Media Publish设置”页面建立了默认设置，用于确定如何将资源从AdobeDynamic Media服务器传递到网站或应用程序。 如果未指定设置，则AdobeDynamic Media服务器将根据“Dynamic Media Publish设置”页面上配置的默认设置交付资源。

另请参阅[可选 — Dynamic Media设置的设置和配置](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)，了解更多可选配置任务。

>[!NOTE]
>
>在Adobe Experience Manager as a Cloud Service上从Dynamic Media Classic升级到Dynamic Media？ Dynamic Media中的[常规设置](/help/assets/dynamic-media/dm-general-settings.md)页面和Publish设置页面已预填充从您的Dynamic Media Classic帐户中获取的值。 例外情况是“常规设置”页面的&#x200B;**[!UICONTROL 默认上载选项]**&#x200B;区域下列出的所有值。 这些值已在Experience Manager中。 因此，您通过Experience Manager用户界面在&#x200B;**[!UICONTROL 默认上传选项]**&#x200B;下对五个选项卡中的任何选项卡所做的任何更改都会反映在Dynamic Media中，而不是Dynamic Media Classic中。 Experience Manager时，[常规设置](/help/assets/dynamic-media/dm-general-settings.md)页面和Publish设置页面中的所有其他设置和值会在Dynamic Media Classic和Dynamic Media之间维护。

**要配置Dynamic Media Publish安装程序图像服务器：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择“工具”图标，然后转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish设置]**。
1. 在“图像服务器”页面中，设置图像服务器 — 发布上下文，然后使用五个选项卡配置默认发布设置。

   * [图像服务器](#image-server)
      * [安全性](#security-tab)选项卡
      * [目录管理](#catalog-management-tab)选项卡
      * [请求属性](#request-attributes-tab)选项卡
      * [常用缩略图属性](#common-thumbnail-attributes-tab)选项卡
      * [色彩管理属性](#color-management-attributes-tab)选项卡

   ![Dynamic Media Publish设置页面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media Publish设置页面，已选择&#x200B;**[!UICONTROL 请求属性]**选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**。

## 图像服务器 {#image-server}

“映像服务器”页建立了从映像服务器传送映像的默认设置。 设置分为五个类别

| 发布上下文 | 描述 |
| --- | --- |
| 图像服务 | 指定发布设置的上下文。 |
| 提供测试图像 | 指定用于测试发布设置的上下文。<br>仅对于新的Dynamic Media帐户，默认&#x200B;**[!UICONTROL 客户端地址]**&#x200B;字段自动设置为`127.0.0.1`。<br>在公开资产之前查看[测试资产](#test-assets-before-making-public)。 |

### “安全”选项卡 {#security-tab}

**[!UICONTROL 客户端地址]** — 允许您指定一个或多个地址或IP地址范围。 指定后，将拒绝从未列出的IP地址上的客户端发出的对此图像目录的请求。 此规则同时适用于交付图像和渲染的图像。

![安全选项卡&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*显示IP“允许”字段的安全选项卡。*


### “目录管理”选项卡 {#catalog-management-tab}

**[!UICONTROL 规则集定义文件路径]** — 指定包含图像目录的规则集定义的文件。

另请参阅《Dynamic Media查看器参考指南》中的[RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html)参数。

>[!NOTE]
>
>如果您的Dynamic Media Classic帐户已选择&#x200B;**[!UICONTROL 规则集定义文件路径]**(在&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序]** > **[!UICONTROL Publish设置]**，在&#x200B;**[!UICONTROL 目录管理]**&#x200B;组下)，则您的Dynamic Media帐户Experience Manager会从Dynamic Media Classic中获取该文件。 当您首次打开&#x200B;**[!UICONTROL Dynamic Media Publish设置]**&#x200B;页面时，该文件将存储并在此字段中可用。

### “请求属性”选项卡 {#request-attributes-tab}

这些设置与图像的默认外观相关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 回复图像大小限制]** | 必需。<br>仅对于新的Dynamic Media帐户，**[!UICONTROL 图像服务]**&#x200B;和&#x200B;**[!UICONTROL 测试图像服务]**&#x200B;的默认大小限制自动设置为宽度： `3000`和高度： `3000`。<br>指定返回给客户端的最大回复图像宽度和高度。 如果请求导致回复图像的宽度或/或高度大于此设置，则服务器会返回错误。<br>另请参阅Dynamic Media查看器参考指南中的[MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html)参数。 |
| **[!UICONTROL 请求混淆模式]** | 如果希望将base64编码应用于有效请求，则启用。<br>另请参阅Dynamic Media查看器参考指南中的[RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html)参数。 |
| **[!UICONTROL 请求锁定模式]** | 如果希望在请求中包含简单的散列锁，则启用。<br>另请参阅《Dynamic Media查看器参考指南》中的[RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html)参数。 |
| **[!UICONTROL 默认请求属性]** | |
| **[!UICONTROL 默认图像文件后缀]** | 必需。<br>附加到目录Path和MaskPath字段值的默认数据文件扩展名（如果路径不包含文件后缀）。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html)参数。 |
| **[!UICONTROL 默认字体名称]** | 指定在文本图层请求未提供字体时使用哪种字体。 如果指定，则它必须是此图像目录的字体映射或默认目录的字体映射中的有效字体名称值。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html)参数。 |
| **[!UICONTROL 默认图像]** | 提供一个默认图像，为响应一个请求而返回，其中未找到所请求的图像。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html)参数。<br>**注意**：如果您的Dynamic Media Classic帐户已选择&#x200B;**[!UICONTROL 默认图像]**(在&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序]** > **[!UICONTROL Publish设置]**，在&#x200B;**[!UICONTROL 默认请求属性]**&#x200B;组下设置)，则您的Dynamic Media帐户将在Experience Manager中从Dynamic Media Classic获取文件。 然后，当您首次打开&#x200B;**[!UICONTROL Dynamic Media Publish设置]**&#x200B;页面时，该文件会被存储并在此字段中可用。 |
| **[!UICONTROL 默认图像模式]** | 启用滑块框（右侧的滑块）后，**[!UICONTROL 默认图像]**&#x200B;会使用默认图像替换源图像中的每个缺失图层，并照常返回复合图像。 禁用滑块框（左侧的滑块）后，默认图像将替换整个复合图像，即使缺少的图像只是多个图层中的一个图层也是如此。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html)参数。 |
| **[!UICONTROL 默认视图大小]** | 必需。<br>仅对于新的Dynamic Media帐户，**[!UICONTROL 图像服务]**&#x200B;和&#x200B;**[!UICONTROL 测试图像服务]**&#x200B;的默认视图大小自动设置为宽度： `1280`和高度： `1280`。<br>如果请求未使用`wid=`、`hei=`或`scl=`明确指定视图大小，服务器将限制回复图像不超过此宽度和高度。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html)参数。 |
| **[!UICONTROL 默认缩略图大小]** | 必需。<br>用于缩略图请求(`req=tmb`)，而不是属性&#x200B;**[!UICONTROL 默认视图大小]**。 如果缩略图请求(`req=tmb`)未使用`wid=`、`hei=`或`scl=`明确指定大小，服务器将限制回复图像不超过此宽度和高度。<br>另请参阅Dynamic Media查看器参考指南中的[DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html)参数。 |
| **[!UICONTROL 默认背景颜色]** | 指定用于填充不包含实际图像数据的回复图像的任意区域的RGB值。<br>另请参阅Dynamic Media查看器参考指南中的[BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html)参数。 |
| **[!UICONTROL 编码属性JPEG]** |  |
| **[!UICONTROL 品质]** | <br>指定JPEG回复图像的默认属性。<br>仅对于新的Dynamic Media帐户，**[!UICONTROL 图像服务]**&#x200B;和&#x200B;**[!UICONTROL 测试图像服务]**&#x200B;的&#x200B;**[!UICONTROL 质量]**&#x200B;默认值自动设置为`80`。<br>此字段定义在1到100的范围内。<br>另请参阅Dynamic Media查看器参考指南中的[JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html)参数。 |
| **[!UICONTROL 色度缩减像素采样]** | 启用或禁用JPEG编码器使用的色度降采样。 |
| **[!UICONTROL 默认重新取样模式]** | 指定用于缩放图像数据的默认重新取样和插值属性。 在请求中未指定`resMode`时使用。<br>仅对于新的Dynamic Media帐户，**[!UICONTROL 图像服务]**&#x200B;和&#x200B;**[!UICONTROL 测试图像服务]**&#x200B;的默认重新取样模式自动设置为`Sharp2`。<br>另请参阅Dynamic Media查看器参考指南中的[ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html)参数。 |

### “常用缩略图属性”选项卡 {#common-thumbnail-attributes-tab}

这些设置与缩略图图像的默认外观和对齐有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 缩略图的默认背景颜色]** | 指定用于填充不包含实际图像数据的输出缩略图图像的区域的RGB值。 仅用于缩略图请求(`req=tmb`)，并且当&#x200B;**[!UICONTROL 默认缩略图类型]**&#x200B;设置设置为&#x200B;**[!UICONTROL 适合]**&#x200B;或&#x200B;**[!UICONTROL 纹理]**&#x200B;时。<br>另请参阅Dynamic Media查看器参考指南中的[ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html)参数。 |
| **[!UICONTROL 水平对齐]** | 指定由`wid=`和`hei=`值指定的回复图像矩形中缩略图图像的水平对齐方式。<br>仅用于缩略图请求(`req=tmb`)，并且当&#x200B;**[!UICONTROL 默认缩略图类型]**&#x200B;设置设置为&#x200B;**[!UICONTROL 适合]**&#x200B;时。<br>有三个水平对齐方式可供选择：**[!UICONTROL 居中对齐]**、**[!UICONTROL 左对齐]**&#x200B;和&#x200B;**[!UICONTROL 右对齐]**。<br>另请参阅Dynamic Media查看器参考指南中的[ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html)参数。 |
| **[!UICONTROL 垂直对齐]** | 指定由`wid=`和`hei=`值指定的回复图像矩形中缩略图图像的垂直对齐方式。 仅用于缩略图请求(`req=tmb`)以及将&#x200B;**[!UICONTROL 默认缩略图类型]**&#x200B;设置设置为&#x200B;**[!UICONTROL 适合]**&#x200B;的情况。<br>有三个垂直对齐方式可供选择：**[!UICONTROL 顶部对齐]**、**[!UICONTROL 居中对齐]**&#x200B;和&#x200B;**[!UICONTROL 底部对齐]**。<br>另请参阅Dynamic Media查看器参考指南中的[ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html)参数。 |
| **[!UICONTROL 默认缓存生存时间]** | 提供特定目录记录中不包含有效目录Expiration值时的默认过期时间间隔（小时）。 设置为`-1`以标记为永不过期。 <br>另请参阅Dynamic Media查看器参考指南中的[过期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html)参数。 |
| **[!UICONTROL 默认缩略图类型]** | 提供特定目录记录中不包含有效目录ThumbType值时的缩略图类型默认值。 仅用于缩略图请求(`req=tmb`)。<br>有三种缩略图类型可供选择： **[!UICONTROL 裁切]**、**[!UICONTROL 适合]**&#x200B;和&#x200B;**[!UICONTROL 纹理]**。<br>另请参阅Dynamic Media查看器参考指南中的[ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html)参数。 |
| **[!UICONTROL 默认缩略图分辨率]** | 提供特定目录记录中不包含有效目录ThumbRes值时的缩略图对象分辨率默认值。 仅用于缩略图请求(`req=tmb`)以及将&#x200B;**[!UICONTROL 默认缩略图类型]**&#x200B;设置设置为&#x200B;**[!UICONTROL 纹理]**&#x200B;的情况。<br>另请参阅Dynamic Media查看器参考指南中的[ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html)参数。 |

### “颜色管理属性”选项卡 {#color-management-attributes-tab}

这些设置确定用于图像的ICC颜色配置文件。

**颜色转换渲染方法**
颜色转换调色(Color Conversion Rendering Intent)允许覆盖工作配置文件的默认调色，以确定如何调整源颜色。 用于以下情况：

1. 默认的ICC配置文件之一是颜色转换的目标颜色空间。
1. 输出设备（打印机或显示器）的特征在于此配置文件。
1. 并且，指定的渲染意图对此配置文件有效。

不同的渲染意图使用不同的规则来确定如何调整源颜色。

另请参阅《Dynamic Media查看器参考指南》中的[IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html)参数。

>[!NOTE]
>
>通常，最好对选定的颜色设置使用默认的调色，该设置已经过Adobe测试以符合行业标准。 例如，如果您为北美或欧洲选择颜色设置，则默认的颜色转换渲染方法为&#x200B;**[!UICONTROL 相对比色]**。 如果您为日本选择了颜色设置，则默认的颜色转换渲染方法为&#x200B;**[!UICONTROL 可感知]**。

| 设置 | 特征 |
| --- | --- |
| **[!UICONTROL CMYK默认颜色空间]** | 指定要用作CMYK数据的工作配置文件的ICC颜色配置文件的名称。 如果选择&#x200B;**[!UICONTROL 无指定]**，则在涉及CMYK源图像时对此图像目录禁用颜色管理。 所有CMYK工作空间都取决于设备，这意味着它们基于实际的油墨和纸张组合。 CMYK工作区Adobe供应基于标准商业打印条件。<br>另请参阅Dynamic Media查看器参考指南中的[IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html)参数。 |
| **[!UICONTROL 默认灰度颜色空间]** | 指定要用作灰度数据的工作配置文件的ICC颜色配置文件的名称。 如果选择&#x200B;**[!UICONTROL 无指定]**，则在涉及灰度源图像时对此图像目录禁用颜色管理。<br>另请参阅Dynamic Media查看器参考指南中的[IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html)参数。 |
| **[!UICONTROL 默认色彩空间]** RGB | 指定要用作RGB数据的工作配置文件的ICC颜色配置文件的名称。 如果选择&#x200B;**[!UICONTROL 无指定]**，则在涉及RGB源图像时对此图像目录禁用颜色管理。 通常，最好选择&#x200B;**[!UICONTROL Adobe RGB]**&#x200B;或&#x200B;**[!UICONTROL sRGB]**，而不是特定设备的配置文件（如监视器配置文件）。 当您为Web或移动设备准备图像时，建议使用&#x200B;**[!UICONTROL sRGB]**，因为它定义了用于在Web上查看图像的标准监视器的颜色空间。 在处理消费者级数码相机的图像时，**[!UICONTROL sRGB]**&#x200B;也是很好的选择，因为大多数此类相机使用sRGB作为默认颜色空间。<br>另请参阅Dynamic Media查看器参考指南中的[IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html)参数。 |
| **[!UICONTROL 颜色转换调色]** | **[!UICONTROL 可感知]** — 旨在保持颜色之间的视觉关系，以便人眼感觉它是自然的，即使颜色值本身可能会发生更改。 此意图适用于具有大量超出色域颜色的照片图像。 该设置是日本印刷业的标准着色。 |
|  | **[!UICONTROL 相对比色]** — 将源颜色空间的极高亮度和目标颜色空间的极高亮度进行比较，并相应地移动所有颜色。 超出色域的颜色将移动到目标色彩空间中最接近的可再现颜色。 相对比色在图像中保留的原始颜色比感知颜色多。 此设置是北美和欧洲打印的标准渲染方法。 |
|  | **[!UICONTROL 饱和度]** — 尝试在图像中生成鲜艳的颜色，而牺牲颜色准确性。 此渲染方法适用于图形或图表等商业图形，在这些图形中，明亮饱和颜色比颜色之间的确切关系更重要。 |
|  | **[!UICONTROL 绝对色度]** — 将落在目标色域中的颜色保持不变。 超出色域的颜色将被剪裁。 不执行将颜色缩放到目标白点的操作。 此意图旨在以保持颜色之间的关系为代价来保持颜色的准确性，并适于进行校样以模拟特定设备的输出。 此意图对于预览纸张颜色对打印颜色的影响非常有用。 |

## 在公开资产之前测试资产 {#test-assets-before-making-public}

Secure Testing可帮助您定义安全的测试环境，并根据一组可配置的IP地址和范围构建强大的企业对企业解决方案。 此功能可让您将AdobeDynamic Media部署与内容管理和业务系统的架构相匹配。

通过Secure Testing，您可以预览包含未发布内容的网站暂存版本。

如有需要，请创建暂存环境，而不是公开资产，原因如下：

* 在公开启动之前预览网站（测试网站）。
* 提供需要受限访问的资产，如在B2B Web应用程序中显示价格的eCatalog。
* 使用防火墙后的资产作为产品信息管理系统、客户服务应用程序、培训网站等的一部分。

>[!NOTE]
>
>安全测试不会影响对Adobe Dynamic Media Classic的访问。 Adobe Dynamic Media Classic安全性将保持一致，并且需要使用常规凭据来访问Adobe Dynamic Media Classic和相关Web服务。

### Secure测试的工作原理 {#how-test-assets-works}

大多数公司都在防火墙后运行互联网。 可以通过特定路由访问Internet，通常通过有限的公共IP地址范围进行访问。

通过公司网络，您可以使用[https://www.whatismyip.com](https://www.whatismyip.com/)之类的网站确定公共IP地址，或者向公司IT组织请求此信息。

通过Secure Testing，AdobeDynamic Media可为暂存环境或内部应用程序建立专用映像服务器。 对此服务器的任何请求都会检查原始IP地址。 如果传入请求不在批准的IP地址列表中，则会返回失败响应。 AdobeDynamic Media公司管理员为公司的Secure Testing环境配置已批准的IP地址列表。

由于必须确认原始请求的位置，因此Secure Testing服务的流量不会像公共Dynamic Media Image Server流量那样通过内容分发网络进行路由。 向Secure Testing服务发出的请求与向公共Dynamic Media图像服务器发出的请求相比，滞后时间稍长一些。

未发布的资产可立即从Secure Testing服务中使用，而无需发布。 通过这种方式，您可以在将资产发布到面向公众的图像服务器之前运行预览。

>[!NOTE]
>
>Secure Testing Services使用配置了内部发布上下文的目录服务器。 因此，如果贵公司配置为发布到Secure Testing，则在AdobeDynamic Media中上传的所有资源都会立即在Secure Testing服务上可用。 不论资源是否标记为在上传时发布，此功能均为true。

安全测试服务当前支持以下资产类型和功能：

* 图像。
* 晕影（渲染服务器请求）。
* 渲染服务器请求（受支持，但必须由客户明确请求）。
* 集，包括图像集、eCatalog、渲染集和媒体集。
* 标准AdobeDynamic Media富媒体查看器。
* AdobeDynamic Media OnDemand JSP页。
* 静态内容，如PDF文件和逐步提供的视频。
* HTTP视频流。
* 渐进式视频流。

当前不支持以下资产类型和功能：

* Adobe Dynamic Media Classic信息或eCatalog搜索
* RTMP视频流
* 网络打印
* UGC（用户生成的内容）服务

  >[!IMPORTANT]
  >
  >从2023年5月1日开始，Dynamic Media中的UGC资源最多可在上传日期起60天内使用。 60天后，将删除资源。

  >[!NOTE]
  >
  >对AdobeDynamic Media中新增或现有UGC矢量图像资源的支持已于2021年9月30日终止。

### 测试Secure Testing服务 {#test-secure-testing-service}

要确保Secure Testing服务按预期工作，请执行以下操作：

#### 准备帐户

1. 请联系Adobe客户关怀部门，要求他们在您的帐户上启用安全测试。
1. 在Adobe Experience Manager中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish设置]**。
1. 在“图像服务器”页面的&#x200B;**[!UICONTROL Publish上下文]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 测试图像服务]**。
1. 选择&#x200B;**[!UICONTROL 安全性]**&#x200B;选项卡。
1. 对于&#x200B;**[!UICONTROL 客户端地址]**&#x200B;筛选器，请选择&#x200B;**[!UICONTROL 添加]**。
1. 在&#x200B;**[!UICONTROL IP地址]**&#x200B;字段中，键入IP地址。
1. 在&#x200B;**[!UICONTROL 掩码]**&#x200B;字段中，键入网络掩码。

   >[!NOTE]
   >
   >如果添加多个IP地址和Net掩码，它将有效地允许&#x200B;*所有*&#x200B;个IP地址进行资产调用，并且这些地址都会显示。

1. 执行下列操作之一：

   * 要添加更多IP地址，请重复前三个步骤。
   * 继续下一步骤。

1. 在“图像服务器”页面的右上角，选择&#x200B;**[!UICONTROL 保存]**。
1. 将所需的图像上传到您的AdobeDynamic Media帐户。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 确保将某些图像标记为发布，将其他图像标记为未标记，然后提交发布作业。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 通过转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media常规设置]**&#x200B;确定Secure Testing服务的名称。
1. 在&#x200B;**[!UICONTROL 服务器]**&#x200B;页面上，找到&#x200B;**[!UICONTROL 已发布的服务器名称]**&#x200B;右侧的服务器名称。

如果Adobe名称缺失或指向服务器的URL不起作用，请联系服务器关怀团队。

#### 准备网站变体

您需要一个网站的两个变体，这两个变体可链接已发布和未发布的资产：

* 公共版本 — 使用传统的AdobeDynamic Media URL语法链接资源。
* 暂存版本 — 使用相同的语法但使用安全测试站点名称链接资产。

#### 运行测试

执行以下测试：

1. 检查资产是否在公司网络中可见。

   在从先前定义的IP地址范围标识的公司网络中，网站的暂存版本会显示所有图像，无论是否标记为发布。 因此，您可以在测试时避免在预览批准或产品发布之前意外使图像可用。

   确认您的网站的公共版本显示已发布的资源，就像之前在AdobeDynamic Media时所做的那样。

1. 在公司网络外部，验证未发布的资产（即未标记为发布的资产）是否受第三方访问的保护。

   从外部访问您的网络（例如，从您的家庭计算机或通过4G/5G连接），然后验证公共版本的网站是否显示所有已发布的资产，但不显示任何未发布的内容。

   确认暂存版本不显示任何资产，因为您正从未批准的IP地址访问Secure Testing服务。
