---
title: 管理数字资源的元数据
description: 了解元数据的类型以及 [!DNL Adobe Experience Manager Assets] 如何帮助管理资源的元数据，以便更轻松地分类和组织资源。 [!DNL Experience Manager] 可以根据资产的元数据自动组织和处理资产。
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management, Metadata
role: User, Architect, Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 9%

---

# 管理数字资源的元数据 {#managing-metadata-for-digital-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Experience Manager Assets]保留每个资源的元数据。 它允许更轻松地分类和组织资产，并帮助查找特定资产的人员。 由于能够从上载到[!DNL Experience Manager Assets]的文件中提取元数据，因此元数据管理与创意工作流集成。 利用使用资源保留和管理元数据的功能，您可以根据资源的元数据自动组织和处理资源。

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 为什么我们需要元数据 {#why-metadata}

元数据是指有关数据的数据。 就这一点而言，数据是指您的数字资产，例如图像。 元数据对于高效的资源管理至关重要。

元数据是某个资源的所有可用数据的集合，但并不一定包含在该图像中。 元数据的一些示例包括：

* 资源的名称。
* 上次修改的时间和日期。
* 资源存储在存储库中的大小。
* 包含它的文件夹的名称。
* 相关资源或应用的标记。

以上是[!DNL Experience Manager]可以管理的资源的基本元数据属性，允许用户查看所有资源。 例如，在尝试发现最近添加或修改的资产时，按上次修改日期对资产排序很有用。

例如，您可以向数字资产添加更多高级数据：

* 资源的类型（是图像、视频、音频剪辑还是文档？）。
* 资产的所有者。
* 资源的标题。
* 资源的描述。
* 分配给资产的标记。

更多元数据可帮助您进一步分类资源，在数字信息量增长时非常有用。 它可以仅根据文件名管理数百个文件。 但是，这种方法不具备扩展性。随着涉及的人数以及管理的资源数的增加，这种方法很快就会出现不足。

随着元数据的增加，数字资源的价值会随之增长，因为资源会变得：

* 更易于访问 - 系统和用户可以轻松地找到它。
* 更易于管理 - 您可以轻松地找到具有一组相同属性的资源并对其应用更改。
* 完整 - 元数据越多，资源就能携带更多信息和具体情境。

出于这些原因，[!DNL Assets]为您提供了创建、管理和交换数字资源元数据的正确方法。

## 元数据的类型 {#types-of-metadata}

元数据分为技术元数据、信息元数据和管理元数据。

### 技术元数据

技术元数据侧重于数字资产的技术方面，提供与以下内容相关的关键信息：

* 文件大小
* 格式
* 解决方法
* 尺寸
* 颜色模式

此类元数据可帮助用户了解并高效使用数字资源。

### 信息元数据

信息性元数据提供描述性信息以增强对内容的理解，有助于内容发现和搜索。 它包括关键字、字幕和描述。 <br>例如，在Experience Manager Assets中管理视频时，我们可以包括以下信息性元数据：

* **关键字**：营销、产品发布、促销
* **Caption**：介绍我们的最新产品以及令人兴奋的功能
* **描述**：视频内容的详细概述。

### 管理元数据

管理元数据涉及数字资产的管理方面。 它确保访问控制、法规遵从性，并管理数字资产管理系统中资产的整个生命周期。 它包括与以下内容相关的信息：

* 资产所有权
* 使用权限
* 权限
* 其他管理详细信息

此元数据类型可确保有效的资源管理、访问控制和法规遵从性。

<!-- Learn more about [metadata best practices](metadata-best-practices.md) to manage your digital assets effectively. -->

<!-- The two basic types of metadata are technical metadata and descriptive metadata.

Technical metadata is useful for software applications that are dealing with digital assets and should not be maintained manually. [!DNL Experience Manager Assets] and other software automatically determine technical metadata and the metadata may change when the asset is modified. The available technical metadata of an asset depends largely on the file type of the asset. Some examples of technical metadata are:

* Size of a file.
* Dimensions (height and width) of an image.
* Bit rate of an audio or video file.
* Resolution (level of detail) of an image.

Descriptive metadata is metadata concerned with the application domain, for example, the business that an asset is coming from. Descriptive metadata cannot be determined automatically. It is created manually or semi-automatically. For example, a GPS-enabled camera can automatically track the latitude and longitude and add geotag the image.

The cost of manually creating descriptive metadata information is high. So, standards are established to ease the exchange of metadata across software systems and organizations. [!DNL Experience Manager Assets] supports all relevant standards for metadata management. -->

## 元数据和上次修改 {#last-modification}

资源的上次修改日期反映了上次修改资源原始文件的时间。 因此，修改日期和用户仅在以下情况下发生更改：

* 上传资源的新版本
* 重新处理资源

上次修改日期和用户未更改：

* 移动或重命名资产时
* 当资产被签出、签入或版本时
* 发布或取消发布资产时
* 关于元数据更新
* 引用或收藏集更新

## 编码标准 {#encoding-standards}

可通过多种方式在文件中嵌入元数据。 支持选择编码标准：

* XMP： [!DNL Assets]用来将提取的元数据存储在存储库中。
* ID3：用于音频和视频文件。
* Exif：用于图像文件。
* 其他/旧版：来自[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是[!DNL Experience Manager Assets]用于所有元数据管理的开放标准。 标准提供了可嵌入到所有文件格式的通用元数据编码。 Adobe和其他公司都支持XMP标准，因为它提供了丰富的内容模型。 XMP Standard和[!DNL Experience Manager Assets]的用户有一个强大的平台可以构建。 有关详细信息，请参阅[XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

当您在计算机上或便携式MP3播放器上播放数字音频文件时，将显示这些ID3标记中存储的数据。

ID3标记是针对MP3文件格式而设计的。 有关格式的其他信息：

* ID3标记可用于MP3和mp3PRO文件。
* WAV没有标记。
* WMA具有不允许开源实施的专有标记。
* Ogg Vorbis使用嵌入到Ogg容器中的Xiph注释。
* AAC使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数字摄影中最常用的元数据格式。 它提供了一种以多种文件格式(如JPEG、TIFF、RIFF和WAV)嵌入元数据属性的固定词汇的方法。 Exif将元数据存储为元数据名称和元数据值对。 这些元数据名称 — 值对也称为标记，不要与[!DNL Experience Manager]中的标记混淆。 现代数码相机创建Exif元数据并提供现代图形软件支持。 Exif格式是元数据管理（尤其是图像）的最低通用分母。

Exif的一个主要限制是一些流行的图像文件格式(如BMP、GIF或PNG)不支持它。

由Exif定义的元数据字段通常具有技术性质，在描述性元数据管理中的用处有限。 因此，[!DNL Experience Manager Assets]提供Exif属性到[通用元数据架构](metadata-schemas.md)和XMP的映射。

#### 其他元数据 {#other-metadata}

可从文件中嵌入的其他元数据包括[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

## 管理数字资源的元数据 {#manage-assets-metadata}

通过Enterprise Manager Assets，可以同时编辑多个资源的元数据，以便快速将常见的元数据更改批量传播到资源。 使用[!UICONTROL 属性]页面将元数据属性更改为通用值或者添加或修改标记。 要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用架构编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或收藏集中可用的资产。 对于跨文件夹可用的资源或与通用条件匹配的资源，可在搜索](/help/assets/search-assets.md#metadata-updates)后[批量更新元数据。

1. 导航到要编辑的资源的位置。
1. 选择要编辑其公共属性的资源。
1. 从工具栏中，选择&#x200B;**[!UICONTROL 属性]**&#x200B;以打开所选资源的[!UICONTROL 属性]页面。

   >[!NOTE]
   >
   >选择多个资源时，将为资源选择最低的常用父表单。 换句话说，[!UICONTROL 属性]页面仅显示所有单独资源的[!UICONTROL 属性]页面中通用的元数据字段。

1. 在各种选项卡下修改所选资源的元数据属性。
1. 要查看特定资源的元数据编辑器，请取消选择列表中剩余的资源。 使用特定资源的元数据填充元数据编辑器字段。

   >[!NOTE]
   >
   >* 在[!UICONTROL 属性]页面中，您可以通过取消选择从资产列表中删除资产。 默认情况下，资源列表已选择所有资源。 您从列表中删除的资产元数据不会更新。
   >* 在资源列表顶部，选中&#x200B;**[!UICONTROL 标题]**&#x200B;附近的复选框，以在选择资源和清除列表之间切换。

1. 要为资源选择其他元数据架构，请从工具栏中选择&#x200B;**[!UICONTROL 设置]**，然后选择所需的架构。 保存更改。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。选择&#x200B;**[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 使用处理配置文件的自定义元数据 {#metadata-compute-service}

Assets as a [!DNL Cloud Service]可以使用云原生服务为资源生成自定义元数据。 配置处理配置文件以生成自定义元数据。 请参阅[如何使用处理配置文件](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

处理配置文件中的![元数据演绎版](assets/processing-profile-metadata.png)

>[!TIP]
>
>一个文件夹只能应用一个处理配置文件。 要将多个处理应用于文件夹中的资产，请向单个处理配置文件添加更多选项。 例如，单个配置文件可以生成演绎版、对资源进行转码、生成自定义元数据等。 您可以为每个任务应用MIME类型过滤器，以便根据所需的文件格式触发相应的任务。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## 元数据架构 {#metadata-schemata}

元数据架构是可在各种应用程序中使用的元数据属性定义的预定义集。 属性始终与资产关联，这意味着属性与资源“关于”。

如果不存在符合您需求的元数据架构，您还可以设计自己的元数据架构。 不要复制现有信息。 在组织内，将架构分隔开可以更轻松地共享元数据。 [!DNL Experience Manager]为您提供了一个最常用元数据架构的默认列表。 列表可帮助您快速启动元数据策略并快速选择所需的元数据属性。

下面列出了支持的元数据架构。

### 标准元数据 {#standard-metadata}

* DC - [!DNL Dublin Core]是一组重要且广泛使用的元数据。
* DICOM — 医学数字成像和通信。
* `Iptc4xmpCore`和`iptc4xmpExt` — 国际新闻通讯标准包含许多特定于主题的元数据。
* RDF — 资源描述框架 — 用于通用语义Web元数据。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ` — 基本作业票证。

### 特定于应用程序的元数据 {#application-specific-metadata}

特定于应用程序的元数据包括技术和描述性元数据。 如果使用此类元数据，则其他应用程序可能无法使用该元数据。 例如，其他图像渲染应用程序可能无法访问[!DNL Adobe Photoshop]元数据。 您可以创建工作流步骤，将特定于应用程序的资产更改为标准资产。

* ACDSee - [!DNL ACDSee]程序管理的元数据。 请参阅[www.acdsee.com/](https://www.acdsee.com/)。
* 相册 — [!DNL Adobe Photoshop Album]。
* CQ — 由[!DNL Experience Manager Assets]使用。
* DAM - [!DNL Experience Manager Assets]使用。
* DEX - [Optima SC Description资源管理器](https://www.optimasc.com/products/dex/index.html)是用于Windows操作系统的元数据和文件管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView媒体专业](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management元数据 {#digital-rights-management-metadata}

* 抄送 — [!DNL Creative Commons]。
* [!DNL XMPRights]。
* 加号 — [图片授权通用系统](https://www.useplus.com)。
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* PRL — 棱镜权限语言。
* PUR - PRISM使用权限。
* `xmpPlus` - PLUS与XMP的集成。

### 特定于照片的元数据 {#photography-specific-metadata}

* Exif — 摄像头提供的技术信息，包括GPS位置。
* CRS - [!DNL Camera Raw]架构。
* `iptc4xmpCore`和`iptc4xmpExt`。
* TIFF — 图像元数据(不仅适用于TIFF图像)。

### 打印特定的元数据 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和第三方应用程序。
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG` — 分页文本的XMP元数据。

### 特定于多媒体的元数据 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media]。
* `xmpMM` — 媒体管理。

## 元数据驱动的工作流 {#metadata-driven-workflows}

创建元数据驱动的工作流可帮助您自动化某些流程，从而提高效率。 在元数据驱动的工作流中，工作流管理系统读取工作流并因此执行一些预定义的操作。 例如，可以使用元数据驱动工作流的某些方法：

* 工作流可以检查图像是否具有标题。 如果不包含，系统会通知您添加标题。
* 工作流可以检查资产上的版权声明是否允许分发。 因此，系统会将资产发送到一台服务器或另一台服务器。
* 工作流可以检查没有预定义的强制性元数据的资源或具有&#x200B;*无效*&#x200B;元数据的资源。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [XMP 元数据](xmp-metadata.md)
>* [如何编辑或添加元数据](meta-edit.md)
