---
title: 管理数字资产的元数据
description: 了解元数据的类型以及AEM资产如何帮助管理资产的元数据，从而更轻松地对资产进行分类和组织。 AEM资产能够保留和管理资产中的任意元数据，因此可以根据资产的元数据自动组织和处理资产。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 管理数字资产的元数据 {#managing-metadata-for-digital-assets}

Adobe Experience Manager(AEM)资产可保留每个资产的元数据。 这使您可以更加方便地分类和组织资产，并且还有助于用户查找特定的资产。元数据管理能够从上传到AEM资产的文件中提取元数据，从而与创意工作流程相集成。 AEM资产能够保留和管理资产中的任意元数据，因此可以根据资产的元数据自动组织和处理资产。

>[!MORELIKETHIS]
>
>* [XMP 元数据](xmp-metadata.md)
>* [如何编辑或添加元数据](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 为何选择元数据 {#why-metadata}

元数据是指关于数据的数据。在这方面，数据是指您处理的资产，例如图像。元数据很重要，因为它使用户可以更高效地管理资产。

元数据是此图像可用的所有数据的集合，但该数据不一定包含在该图像中，例如：

* 资产的名称
* 资产的上次修改日期和时间
* 图像在存储库中的存储大小
* 资产所在的文件夹名称

这些是AEM可以为资产管理的基本元数据属性，通过这些属性，用户可以查看所有资产（例如，按资产的上次修改日期排序）-在尝试发现最近添加到存储库的资产时非常有用。

您可以向数字资产中添加更多高级别的数据，例如：

* 资产的类型（它是图像、视频、音频剪辑，还是文档？）
* 资产的所有者
* 资产的标题
* 资产的描述
* 为资产分配的标记

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。尽管一位用户可以只根据文件名管理数百个文件的列表，但当参与文件管理的用户数和所管理资产的数量增多时，这种方法便不尽如人意了。

向资产中添加元数据后，资产会变得更有价值，因为资产会在以下方面得到改进

* 更易于访问 - 用户可以更轻松地查找资产
* 更易于管理 - 您可以更轻松地查找具有相同属性集的资产，并对它们应用更改
* 更复杂 - 向资产中添加的元数据越多，元数据管理就会变得越重要

鉴于这些原因，AEM 资产为您提供了用于创建、管理和交换数字资产元数据的正确方法。

## Metadata basics {#metadata-basics}

在导入（摄取）资产时，会从资产中提取元数据。此外，添加元数据还可帮助您进一步对资产分类。

本节介绍元数据的类型和编码标准。

### 技术性元数据 {#technical-metadata}

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。技术性元数据可以由 AEM 资产和其他软件自动确定，并且可以在修改资产时进行更改。资产的可用技术性元数据主要取决于资产的文件类型。技术性元数据的示例如下：

* 文件的大小
* 图像的尺寸（高和宽）
* 音频或视频文件的比特率
* 图像的分辨率（细节级别）

### 描述性元数据 {#descriptive-metadata}

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它必须以手动或半自动方式创建。例如，启用了 GPS 的照相机可以自动跟踪拍摄图像时所处的经度和纬度，并将此信息添加到图像的元数据。

由于创建描述性元数据信息需要手动操作，人工成本较高，因此人们建立了相关标准，以便于在软件系统和组织之间交换元数据。

AEM 资产支持元数据管理方面的所有相关标准。

鉴于元数据的重要性，以及创建元数据需要很大的手动工作量，人们建立了相关标准，以便于简化元数据交换。

### Encoding standards {#encoding-standards}

向文件中嵌入元数据的方法有很多种。支持一系列编码标准选项：

* XMP：由 AEM 资产用来在存储库中存储提取的元数据。
* ID3：适用于音频和视频文件。
* EXIF：适用于图像文件。
* 其他／旧版：Microsoft Word、PowerPoint、Excel等。

#### XMP {#xmp}

XMP是指可扩展元数据平台，是AEM资产用于所有元数据管理的元数据标准。除了提供可嵌入到所有文件格式的通用元数据编码外，XMP还提供丰富的内容模型，并且受Adobe和其他公司的支持，因此XMP用户与AEM Assets的结合具有强大的构建平台。

#### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3 标记适用于 MP3 和 MP3pro 文件。
* WAV 无标记。
* WMA 使用专有标记，不允许开源实现。
* Ogg Vorbis使用嵌入在OGG容器中的Xiph注释。
* AAC 使用专有标记格式。

#### EXIF {#exif}

EXIF 是指可交换图像文件格式，它是数字摄影领域最常用的元数据格式。通过 EXIF，可以在多种文件格式中嵌入固定的元数据属性词汇，例如：

* JPEG
* TIFF
* RIFF
* WAV

EXIF 的主要局限性在于，其他一些常用的图像文件格式（例如，BMP、GIF 或 PNG）不支持这种编码标准。

EXIF 将元数据存储为元数据名称和元数据值对。这些元数据名称-值对也称为标记，但切勿将其与 AEM 中的标记混淆。

由于 EXIF 是由现代数码相机自动创建，并通过现代图形软件来支持，因此它在元数据管理中可被视为最不常用的标准。

由 EXIF 定义的大多数元数据字段都具有很强的技术性，并且在描述性元数据管理方面的作用比较有限。For this reason, AEM Assets offers mapping of EXIF properties into [common metadata schemata](metadata-schemas.md) and into [XMP](xmp-metadata.md), the powerful metadata format AEM Assets uses for metadata management.

#### 其他元数据 {#other-metadata}

可以从文件中嵌入的其他元数据包括Microsoft Word、PowerPoint、Excel等。

## 管理数字资产的元数据 {#manage-assets-metadata}

Enterprise Manager资产允许您同时编辑多个资产的元数据，以便快速将常见元数据更改批量传播到资产。 使用“ [!UICONTROL 属性] ”页可将元数据属性更改为通用值，或添加或修改标记。 要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用架构编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](/help/assets/search-assets.md#metadataupdates)。

1. 导航到要编辑的资产所在的位置。
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，点按／单 **[!UICONTROL 击属性]** ，以打开选 [!UICONTROL 定资产的] “属性”页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最低级别的父表单。 换句话说，“属 [!UICONTROL 性] ”页面仅显示所有单个资产的“属性”页  面中通用的元数据字段。

1. 修改各个选项卡下选定资产的元数据属性。
1. 要查看特定资产的元数据编辑器，请取消选择列表中的其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在“属 [!UICONTROL 性] ”页面中，您可以通过取消选择资产来从资产列表中删除资产。 默认情况下，资产列表会选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. 要为资产选择其他元数据架构，请点按／单击工 **[!UICONTROL 具栏中的]** “设置”，然后选择所需的架构。 保存更改。
1. 要将新元数据与包含多个值的字段中的现有元数据一起追加，请选择“ **[!UICONTROL 追加”模式]**。 如果不选择此选项，则新元数据将替换字段中的现有元数据。 点按／单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择“追加”模式，新元数据也不会附加到字段中的现有 **[!UICONTROL 值中]**。

## 配置批量元数据更新限制 {#configlimit}

为防止出现类似DOS的情况，AEM限制了Sling请求中支持的参数数。 在一次性更新许多资产的元数据时，您可能会达到限制，并且不会更新更多资产的元数据。 AEM在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

要更改限制，请访问Web控制台( **[!UICONTROL “工具]** ”>“操作” **[!UICONTROL >]** Web Prosements **[!UICONTROL )，并更改]********** Apache Sling Handling Signi配置中Maximum POST Parameters PrametersInternts Apache Shandling Osgi Configuration的值。

## 元数据架构 {#metadata-schemata}

元数据架构是指预定义的元数据属性定义集，可用在很多种应用程序中。属性始终与资产相关联，也就是说属性是“关于”资源的数据。

如果不存在能满足您需求的元数据架构，您也可以自行设计元数据架构（但是，请注意避免创建与已有架构重复的内容）。在组织内部对架构予以划分，可简化各组织之间的元数据共享。

AEM为您提供了最流行的元数据架构的现成列表，允许您快速启动元数据策略并从已定义的架构中选取所需的元数据属性。

下一节列出了支持的元数据架构。

### 标准元数据 {#standard-metadata}

* dc - 都柏林核心 - 最重要、应用最广泛的元数据集
* DICOM - 医学数字成像和通信
* Iptc4xmpCore 和 iptc4xmpExt - 国际媒体通信标准 - 许多特定于主题的元数据
* rdf - 资源描述框架 - 适用于通用语义 Web 元数据
* xmp - 可扩展元数据平台
* xmpBJ - 基本工单

### 特定于应用程序的元数据 {#application-specific-metadata}

>[!NOTE]
>
>特定于应用程序的元数据包括技术性元数据和描述性元数据。如果您使用这类元数据，其他应用程序将无法使用这些元数据。例如，如果您的某个资产使用 Adobe Photoshop 元数据，则当其他图像渲染应用程序尝试访问该资产的元数据时，便无法访问这些元数据。
>
>如果您发现您的资产中有很多特定于应用程序的元数据，您可以创建一个工作流步骤，将特定于应用程序的属性更改为标准属性。

* acdsee - metadata managed by the ACDSee program [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq —— 由AEM资产使用
* dam - 由 AEM 资产使用
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto 和 MP - Microsoft Photo
* pdf 和 pdfx
* photoshop 和 psAux - Adobe Photoshop

### 数字权限管理元数据 {#digital-rights-management-metadata}

* cc - Creative Commons
* xmpRights
* plus —— 图片授权通用系统- https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata行业标准元数据的发布要求
* prl - Prism 权限语言
* pur - Prism 使用权限
* xmpPlus - PLUS 与 XMP 的集成

### 特定于摄影领域的元数据 {#photography-specific-metadata}

* exif - 照相机中的大量技术性信息，包括 GPS 定位
* crs - Photoshop Camera Raw
* Iptc4xmpCore和iptc4xmpExt
* TIFF - 图像元数据（并非只适用于 TIFF 图像）

### 特定于打印领域的元数据 {#print-specific-metadata}

* pdf和pdfx - Adobe PDF和第三方应用程序
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata
* xmp
* xmpPG - 适用于分页文本的 xmp

### Multimedia-specific metadata {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - 媒体管理

## Metadata-driven workflows {#metadata-driven-workflows}

创建元数据驱动的工作流可以帮助您实现一些流程的自动化，从而提高效率。在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。

例如，以下是可以利用元数据驱动的工作流实现的功能：

* 该工作流可以检查图像是否含有标题。如果图像没有标题，系统会通知特定用户添加标题。
* 该工作流可以检查资产上的版权声明是否允许分发。如果允许分发，系统会将资产发送到某台服务器。如果不允许分发，系统会将资产发送到另一台服务器。
