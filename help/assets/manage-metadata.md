---
title: 管理数字资产的元数据
description: 了解元数据的类型，以及如何 [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 根据资产的元数据自动组织和处理资产。
contentOwner: AG
mini-toc-levels: 1
feature: 资产管理，元数据
role: 业务从业者，架构师，管理员
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 15%

---


# 管理数字资产的元数据{#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 为每个资产保留元数据。它可以更轻松地对资产进行分类和组织，并帮助寻找特定资产的用户。 元数据管理能够从上传到[!DNL Experience Manager Assets]的文件中提取元数据，与创意工作流程集成。 利用资产中的元数据保留和管理功能，您可以根据资产的元数据自动组织和处理资产。

>[!MORELIKETHIS]
>
>* [XMP 元数据](xmp-metadata.md)
>* [如何编辑或添加元数据](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 为何需要元数据 {#why-metadata}

元数据是指关于数据的数据。在这方面，数据是指您的数字资产，如图像。 元数据对于有效管理资产至关重要。

元数据是资产可用的所有数据的集合，但该数据不一定包含在该图像中。 一些元数据示例包括：

* 资产的名称。
* 上次修改的时间和日期。
* 资源在存储库中存储时的大小。
* 它所包含的文件夹的名称。
* 相关资产或已应用的标记。

以上是[!DNL Experience Manager]可以为资产管理的基本元数据属性，用户可通过这些属性查看所有资产。 例如，在尝试发现最近添加的资产时，按上次修改日期对资产进行排序非常有用。

您可以向数字资产中添加更多高级别的数据，例如：

* 资源的类型(是图像、视频、音频剪辑还是文档?)。
* 资产的所有者。
* 资产的标题。
* 资产的描述。
* 为资产分配的标记。

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。仅根据文件名管理数百个文件是可能的。 但是，此方法不可扩展。 当相关人员数量和管理资产数量增加时，这个数字还不够。

随着元数据的添加，数字资产的价值会随之增长，因为

* 更易于访问 — 系统和用户可以轻松找到它。
* 更易于管理 — 您可以更轻松地查找具有相同属性集的资产，并将更改应用于这些资产。
* 完整 — 资产包含更多信息和上下文，并包含更多元数据。

出于这些原因，[!DNL Assets]为您提供了创建、管理和交换数字资产元数据的正确方法。

## 元数据的类型 {#types-of-metadata}

两种基本类型的元数据是技术性元数据和描述性元数据。

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。[!DNL Experience Manager Assets] 而其他软件会自动确定技术性元数据，并且修改资产时，元数据可能会发生更改。资产的可用技术性元数据主要取决于资产的文件类型。技术元数据的一些示例包括：

* 文件的大小。
* Dimension（高度和宽度）。
* 音频或视频文件的比特率。
* 图像的分辨率（细节级别）。

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它是手动或半自动创建的。 例如，启用GPS的相机可自动跟踪经纬度并添加地理标记图像。

手动创建描述性元数据信息的成本很高。 因此，我们建立了各种标准来简化跨软件系统和组织的元数据交换。 [!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

## 编码标准{#encoding-standards}

在文件中嵌入元数据有多种方式。 支持一系列编码标准选项：

* XMP:由[!DNL Assets]用来在存储库中存储提取的元数据。
* ID3：适用于音频和视频文件。
* Exif:。
* 其他/旧版：从[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一个开放标准，可供所有元 [!DNL Experience Manager Assets] 数据管理使用。标准优惠可嵌入所有文件格式的通用元数据编码。 Adobe和其他公司支持XMP标准，因为它提供了丰富的内容模型。 XMP标准版和[!DNL Experience Manager Assets]版的用户拥有强大的平台，可以在此基础上进行构建。 有关详细信息，请参阅[XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3标记适用于MP3和mp3PRO文件。
* WAV 无标记。
* WMA具有不允许开放源代码实现的专有标签。
* Ogg Vorbis 使用嵌入在 Ogg 容器中的 Xiph 注释。
* AAC 使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数码摄影中最常用的元数据格式。 它提供了一种将固定的元数据属性词汇嵌入多种文件格式（如JPEG、TIFF、RIFF和WAV）的方法。 Exif将元数据存储为元数据名称和元数据值对。这些元数据名称 — 值对也称为标记，请勿与[!DNL Experience Manager]中的标记混淆。 现代数码相机创建Exif元数据，现代图形软件支持它。 Exif格式是元数据管理（尤其是图像）的最小公分母。

Exif的一个主要限制是一些常用的图像文件格式（如BMP、GIF或PNG）不支持它。

Exif定义的元数据字段通常是技术性的，在描述性元数据管理中的用途有限。 因此，[!DNL Experience Manager Assets]将Exif属性映射到[常见元数据架构](metadata-schemas.md)和XMP。

#### 其他元数据{#other-metadata}

可以从文件中嵌入的其他元数据包括[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

## 管理数字资产的元数据{#manage-assets-metadata}

Enterprise Manager资产允许您同时编辑多个资产的元数据，以便您可以快速将常见元数据更改批量传播到资产。 使用[!UICONTROL “属性”]页可将元数据属性更改为通用值，或添加或修改标记。 要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用模式编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或收藏集中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可以在搜索](/help/assets/search-assets.md#metadata-updates)后，[批量更新元数据。

1. 导航到要编辑的资产所在的位置。
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，点按/单击&#x200B;**[!UICONTROL 属性]**&#x200B;以打开选定资产的[!UICONTROL 属性]页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最常用的父表单。 换言之，“[!UICONTROL 属性]”页面仅显示所有单个资产的[!UICONTROL 属性]页面中通用的元数据字段。

1. 在各种选项卡下修改选定资产的元数据属性。
1. 要视图特定资产的元数据编辑器，请取消在列表中选择其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在[!UICONTROL 属性]页面中，可以通过取消选择从资产列表中删除资产。 资产列表会默认选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* 在资产列表的顶部，选中&#x200B;**[!UICONTROL 标题]**&#x200B;附近的复选框，可在选择资产和清除列表之间切换。


1. 要为资产选择其他元数据模式，请点按/单击工具栏中的&#x200B;**[!UICONTROL 设置]**，然后选择所需的模式。 保存更改。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。点按／单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 使用处理用户档案{#metadata-compute-service}的自定义元数据

作为[!DNL Cloud Service]的资产可以使用云本机服务为资产生成自定义元数据。 配置处理用户档案以生成自定义元数据。 请参阅[如何使用处理用户档案](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

![处理用户档案中的元数据再现](assets/processing-profile-metadata.png)

>[!TIP]
>
>只能将一个处理用户档案应用于文件夹。 要对文件夹中的资产应用多个处理，请向单个处理用户档案添加更多选项。 例如，单个用户档案可以生成演绎版、转码资产、生成自定义元数据等。 您可以对每个任务应用MIME类型过滤器，以便为所需的文件格式触发相应的任务。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## 元数据架构{#metadata-schemata}

元数据模式是可用于各种应用程序的预定义元数据属性定义集。 属性始终与资产关联，这意味着属性是“关于”资源。

如果不存在能满足您需求的元数据架构，您还可以设计自己的元数据架构。 请勿重复现有信息。 在组织内对架构进行划分，可更轻松地共享元数据。 [!DNL Experience Manager] 为您提供最常用元数据架构的默认列表。该列表可帮助您快速启动元数据战略并快速选择所需的元数据属性。

支持的元数据架构如下所列。

### 标准元数据{#standard-metadata}

* DC - [!DNL Dublin Core]是一组重要且广泛使用的元数据。
* DICOM - 医学数字成像和通信.
* `Iptc4xmpCore` and -  `iptc4xmpExt` International Press Communications Standard包含许多特定主题的元数据。
* RDF — 资源描述框架 — 用于通用语义Web元数据。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本工单。

### 特定于应用程序的元数据{#application-specific-metadata}

特定于应用程序的元数据包括技术和描述性元数据。 如果您使用此类元数据，其他应用程序可能无法使用该元数据。 例如，其他图像渲染应用程序可能无法访问[!DNL Adobe Photoshop]元数据。 您可以创建一个工作流步骤，该步骤将应用程序特定属性更改为标准属性。

* ACDSee — 由[!DNL ACDSee]项目管理的元数据。 请参阅[www.acdsee.com/](https://www.acdsee.com/)。
* 影集 — [!DNL Adobe Photoshop Album]。
* CQ — 由[!DNL Experience Manager Assets]使用。
* DAM — 由[!DNL Experience Manager Assets]使用。
* DEX - [Optima SC描述资源管理器](http://www.optimasc.com/products/dex/index.html)是用于Windows操作系统元数据和文件管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management元数据{#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* PLUS - [图片授权通用系统](https://www.useplus.com)。
* PRISM - [行业标准元数据发布要求](https://www.idealliance.org/prism-metadata)。
* PRL - PRISM权限语言。
* PUR - PRISM使用权限。
* `xmpPlus`  — 将PLUS与XMP集成。

### 特定于摄影的元数据{#photography-specific-metadata}

* Exif — 相机中的技术信息，包括GPS定位。
* CRS - [!DNL Camera Raw]模式。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 图像元数据（不仅适用于TIFF图像）。

### 特定于打印的元数据{#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和第三方应用程序。
* PRISM - [行业标准元数据发布要求](https://www.idealliance.org/prism-metadata)。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG`  — 分页文本的XMP元数据。

### 特定于多媒体的元数据{#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 媒体管理。

## 元数据驱动的工作流{#metadata-driven-workflows}

创建元数据驱动的工作流可以帮助您实现一些流程的自动化，从而提高效率。 在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。例如，以下是可以利用元数据驱动的工作流实现的功能：

* 工作流可以检查图像是否具有标题。 如果没有，系统将通知您添加标题。
* 该工作流可以检查资产上的版权声明是否允许分发。 因此，系统会将资产发送给一台或另一台服务器。
* 工作流可以检查没有预定义的强制元数据的资产，或具有&#x200B;*无效*&#x200B;元数据的资产。
