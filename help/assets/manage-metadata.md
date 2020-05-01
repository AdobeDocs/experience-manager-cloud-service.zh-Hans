---
title: 在[!DNL Adobe Experience Manager]中管理数字资产的元数据。
description: 了解元数据的类型以及[!DNL Adobe Experience Manager资产]如何帮助管理资产的元数据，从而更轻松地对资产进行分类和组织。 [!DNL Experience Manager]允许根据资产的元数据自动组织和处理资产。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# 管理数字资产的元数据 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 为每个资产保留元数据。 这可以更轻松地对资产进行分类和组织，并帮助寻找特定资产的用户。 With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

>[!MORELIKETHIS]
>
>* [XMP 元数据](xmp-metadata.md)
>* [如何编辑或添加元数据](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 为何选择元数据 {#why-metadata}

元数据是指关于数据的数据。在这方面，数据是指您的数字资产，如图像。 元数据对于有效管理资产至关重要。

元数据是资产可用的所有数据的集合，但该数据不一定包含在该图像中。 一些元数据示例包括：

* 资产的名称。
* 上次修改的时间和日期。
* 资产存储在存储库中时的大小。
* 其所包含的文件夹的名称。
* 相关资产或已应用的标记。

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

您可以向数字资产中添加更多高级别的数据，例如：

* 资源类型(它是图像、视频、音频剪辑还是文档?)。
* 资产的所有者。
* 资产的标题。
* 资产的描述。
* 分配给资产的标记。

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。仅根据文件名管理数百个文件是可能的。 但是，这种方法不具有可扩展性，而且当所涉人员数量和管理资产数量增加时，这种方法会很快落空。

随着元数据的添加，数字资产的价值会增加，因为资产会变得

* 更易于访问——系统和用户可以轻松找到它。
* 更易于管理——您可以更轻松地查找具有相同属性集的资产，并将更改应用到这些资产。
* 更完整——您向资产添加的元数据越多，其中包含的信息和上下文也就越多。

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## 元数据的类型 {#types-of-metadata}

两种基本类型的元数据是技术性元数据和描述性元数据。

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。[!DNL Experience Manager Assets] 而其他软件会自动确定技术性元数据，并且修改资产时，元数据可能会发生更改。 资产的可用技术性元数据主要取决于资产的文件类型。技术元数据的一些示例包括：

* 文件的大小。
* 图像的尺寸（高度和宽度）。
* 音频或视频文件的比特率。
* 图像的分辨率（详细程度）。

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它是手动或半自动创建的。 例如，启用GPS的相机可自动跟踪经纬度并添加地理标记图像。

由于创建描述性元数据信息需要手动操作，人工成本较高，因此人们建立了相关标准，以便于在软件系统和组织之间交换元数据。

[!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

鉴于元数据的重要性，以及创建元数据需要很大的手动工作量，人们建立了相关标准，以便于简化元数据交换。

## Encoding standards {#encoding-standards}

在文件中嵌入元数据有多种方法。 支持一系列编码标准选项：

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：适用于音频和视频文件。
* Exif: 。
* 其他／旧版： 从 [!DNL Microsoft Word]、 [!DNL PowerPoint][!DNL Excel]等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一个开放标准，用于所 [!DNL Experience Manager Assets] 有元数据管理。 标准优惠可嵌入到所有文件格式的通用元数据编码。 Adobe和其他公司支持XMP标准，因为它提供丰富的内容模型。 XMP标准和的用户 [!DNL Experience Manager Assets] 拥有强大的基础平台。 有关详细信息，请参 [阅XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3标记在MP3和mp3PRO文件中有效。
* WAV 无标记。
* WMA具有不允许开放源码实现的专有标签。
* Ogg Vorbis 使用嵌入在 Ogg 容器中的 Xiph 注释。
* AAC 使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数字摄影中最常用的元数据格式。 它提供了一种在多种文件格式（如JPEG、TIFF、RIFF和WAV）中嵌入固定的元数据属性词汇的方法。 Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager]. 由于Exif是由现代数码相机自动创建并通过现代图形软件提供支持的，因此它被视为元数据管理的最低标准。

Exif的一个主要限制是一些常用的图像文件格式（如BMP、GIF或PNG）不支持它。

通常由Exif定义的元数据字段在性质上是技术性的，在描述性元数据管理中的用途有限。 因此，将Exif属 [!DNL Experience Manager Assets] 性映射到通用元数 [据架构和](metadata-schemas.md) XMP中的优惠。

#### Other metadata {#other-metadata}

可以从文件中嵌入的其他元数据包括Microsoft Word、PowerPoint、Excel等。

## 管理数字资产的元数据 {#manage-assets-metadata}

Enterprise Manager资产允许您同时编辑多个资产的元数据，以便快速将常见元数据更改批量传播到资产。 使用“ [!UICONTROL 属性] ”页可将元数据属性更改为通用值，或添加或修改标记。 要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用模式编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](/help/assets/search-assets.md#metadataupdates)。

1. 导航到要编辑的资产所在的位置。
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，点按／单 **[!UICONTROL 击属]** 性以打开 [!UICONTROL 选定资] 产的“属性”页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最常见的父表单。 换言之，“属 [!UICONTROL 性] ”页面仅显示所有单个资产的“属 [!UICONTROL 性] ”页面中通用的元数据字段。

1. 修改各个选项卡下选定资产的元数据属性。
1. 要视图特定资产的元数据编辑器，请在列表中取消选择其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在“属 [!UICONTROL 性] ”页面中，您可以通过取消选择资产来从资产列表中删除资产。 默认情况下，资产列表会选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. 要为资产选择其他元数据模式，请点按／单 **[!UICONTROL 击工]** 具栏中的设置，然后选择所需的模式。 保存更改。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。点按／单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 配置元数据批量更新限制 {#configlimit}

为防止出现类似DOS的情况，AEM限制了Sling请求中支持的参数数。 在一次性更新多个资产的元数据时，您可能会达到限制，并且不会更新更多资产的元数据。 AEM会在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

要更改限制，请访问 Web Console（**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web Console]**），更改 ]**Apache Sling 请求参数处理]** OSGi 配置中的&#x200B;**[!UICONTROL 最大 POST 参数**[!UICONTROL &#x200B;值。

## Metadata schemata {#metadata-schemata}

元数据模式是预定义的元数据属性定义集，可用于各种应用程序。 属性始终与资产关联，这意味着属性是资源的“关于”。

如果不存在能满足您需求的元数据架构，您还可以设计自己的元数据架构。 请勿重复现有信息。 在组织内，将架构分开，可更轻松地共享元数据。 [!DNL Experience Manager] 为您提供最常用元数据架构的默认列表。 该列表可帮助您快速启动元数据战略并快速选择所需的元数据属性。

支持的元数据架构列于下面。

### Standard metadata {#standard-metadata}

* dc - [!DNL Dublin Core] is the most important and widely used set of metadata.
* DICOM - 医学数字成像和通信.
* Iptc4xmpCore和iptc4xmpExt - International Press Communications Standard包含许多特定于主题的元数据。
* rdf - 资源描述框架 - 适用于通用语义 Web 元数据.
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - 基本工单.

### Application-specific metadata {#application-specific-metadata}

特定于应用程序的元数据包括技术性元数据和描述性元数据。 如果您使用这类元数据，其他应用程序将无法使用这些元数据。For example, if you have an asset with [!DNL Adobe Photoshop] metadata and another image-rendering application tries to access the metadata, it may not be able to access the metadata. 如果您发现资产中有许多特定于应用程序的元数据，则可以创建一个工作流步骤，将特定于应用程序的属性更改为标准属性。

* ACDSee —— 由项目管理的元 [!DNL ACDSee] 数据。 请参 [阅www.acdsee.com/](https://www.acdsee.com/)。
* album - [!DNL Adobe Photoshop Album]。
* cq - Used by [!DNL Experience Manager Assets].
* dam —— 使用方 [!DNL Experience Manager Assets]。
* dex - Optima SC Description Explorer.
* crs - Adobe Photoshop Camera Raw.
* lr - [!DNL Adobe Lightroom]
* mediapro - IView MediaPro.
* MicrosoftPhoto 和 MP - Microsoft Photo.
* pdf 和 pdfx.
* photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* plus - [Picture Licensing Universal System](https://www.useplus.com).
* prism - https://www.idealliance.org/prism-metadata行业标准元数据的发布要求。
* PRL - PRISM权限语言。
* PUR - PRISM使用权。
* xmpPlus - PLUS与XMP集成。

### Photography-specific metadata {#photography-specific-metadata}

* Exif —— 相机技术信息，包括GPS定位。
* CRS - [!DNL Camera Raw] 模式
* Iptc4xmpCore和iptc4xmpExt。
* TIFF —— 图像元数据（不仅适用于TIFF图像）。

### Print-specific metadata {#print-specific-metadata}

* pdf和pdfx - Adobe PDF和第三方应用程序。
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata.
* XMP.
* xmpPG —— 针对分页文本的XMP元数据。

### Multimedia-specific metadata {#multimedia-specific-metadata}

* xmpDM - [!DNL Dynamic Media].
* xmpMM - 媒体管理.

## Metadata-driven workflows {#metadata-driven-workflows}

创建元数据驱动的工作流可以帮助您实现一些流程的自动化，从而提高效率。 在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。例如，以下是可以利用元数据驱动的工作流实现的功能：

* 该工作流可以检查图像是否具有标题。 如果没有，系统将通知您添加标题。
* 该工作流可以检查资产上的版权声明是否允许分发。 因此，系统将资产发送给一台或另一台服务器。
* 工作流可以检查没有预定义的强制元数据的资产，或具有无效元数据 *的资产* 。
