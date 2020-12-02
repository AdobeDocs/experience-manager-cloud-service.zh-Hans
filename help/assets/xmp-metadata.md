---
title: XMP 元数据
description: 了解用于元数据管理的XMP（可扩展元数据平台）元数据标准。 AEM将其用作元数据的创建、处理和交换的标准格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 54%

---


# XMP 元数据 {#xmp-metadata}

XMP（可扩展元数据平台）是 AEM 资产用来进行所有元数据管理的元数据标准。XMP 为在各种应用程序中创建、处理和交换元数据提供了一种标准格式。

除了提供可嵌入到所有文件格式的通用元数据编码外，XMP还提供丰富的[内容模型](#xmp-core-concepts)，并且受Adobe](#advantages-of-xmp)和其他公司的支持[，使XMP与AEM Assets联合的用户拥有强大的基础平台。

## XMP概述和生态系统{#xmp-ecosystem}

AEM Assets本机支持XMP元数据标准。 XMP是处理和存储数字资产中标准化的专有元数据的标准。 XMP 旨在形成通用标准，从而让多个应用程序能够高效地处理元数据。

例如，专业生产人士可以使用 Adobe 应用程序中内置的 XMP 支持，在多种文件格式之间传递信息。AEM 资产存储库会提取 XMP 元数据，用它来管理内容生命周期，并提供创建自动化工作流的能力。

XMP 通过提供数据模型、存储模型和架构，使元数据的定义、创建和处理方式实现标准化。本节将介绍所有这些概念。

来自 EXIF、ID3 或 Microsoft Office 的所有旧版元数据都将自动转换为 XMP，而 XMP 可进行扩展，以支持特定于客户的元数据架构，例如产品目录。

XMP 中的元数据包含一组属性。这些属性始终与称为资源的特定实体相关联；即，属性是“关于”资源的。 对于 XMP，资源始终是指资产。

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP 的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP 具有以下优势：

* 基于 XMP 的元数据非常强大且精细。
* XMP 允许您为一个属性设置多个值。
* XMP 采用标准化的编码，让您可以轻松交换元数据。
* XMP 具有可扩展性。您可以向资产中添加其他信息。

XMP标准设计为可扩展，允许您向XMP数据中添加自定义类型的元数据。 而EXIF则不然——它具有无法扩展的属性的固定列表。

>[!NOTE]
>
>XMP 一般不允许嵌入二进制类型的数据。要在XMP中包含二进制数据（例如缩略图），必须以XML友好格式（如`Base64`）对它们进行编码。

### XMP核心概念{#xmp-core-concepts}

**命名空间和架构**

XMP 架构是通用 XML 命名空间中的一组属性名称，包括数据类型和描述性信息。
XMP 架构采用其 XML 命名空间 URI 进行标识。使用命名空间可以防止不同架构内名称相同但含义不同的属性之间发生冲突。

例如，在两个独立设计的架构中，**创建者**&#x200B;属性可能指创建资产的人，也可能指创建资产的应用程序（例如，Adobe Photoshop）。

**XMP属性和值**

XMP 可以包含来自一个或多个架构的属性。例如，很多 Adobe 应用程序使用的典型子集包括以下架构：

* 都柏林核心模式:`dc:title`、`dc:creator`、`dc:subject`、`dc:format`、`dc:rights`
* XMP基本模式:`xmp:CreateDate`、`xmp:CreatorTool`、`xmp:ModifyDate`、`xmp:metadataDate`
* XMP rights management模式:`xmpRights:WebStatement`, `xmpRights:Marked`
* XMP媒体管理模式:`xmpMM:DocumentID`

**替代语言**

XMP 支持向文本属性添加 `xml:lang` 属性以指定文本的语言。

## XMP 写回到演绎版 {#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)资产中的此XMP回写功能可将资产元数据更改复制到资产的演绎版。

当您从AEM Assets内更改资产的元数据或在上传资产时，更改最初存储在CRXDE的资产节点内。

XMP回写功能会将元数据更改传播到资产的所有或特定演绎版。

请考虑将标题为`Classic Leather`的资产的[!UICONTROL Title]属性修改为`Nylon`的情况。

![元数据](assets/metadata.png)

在这种情况下，AEM Assets会为资产层次结构中存储的资产元数据在`dc:title`参数中保存对&#x200B;**[!UICONTROL Title]**&#x200B;属性所做的更改。

![metadata_stored](assets/metadata_stored.png)

但是，AEM Assets不会自动将任何元数据更改传播到资产的演绎版。

XMP回写功能允许您将元数据更改传播到资产的所有或特定演绎版。 但是，这些更改不会存储在资产层次结构中的元数据节点下。此功能而是会将更改嵌入到演绎版的二进制文件中。

### 启用XMP写回{#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

要在上传元数据更改时将其传播到资产的演绎版，请修改Configuration Manager中的&#x200B;**[!UICONTROL Adobe CQDAM演绎版制作器]**&#x200B;配置。

1. 要打开Configuration Manager，请访问`https://[aem_server]:[port]/system/console/configMgr`。
1. 打开&#x200B;**[!UICONTROL Adobe CQDAM再现制造商]**&#x200B;配置。
1. 选择&#x200B;**[!UICONTROL 传播XMP]**&#x200B;选项，然后保存更改。

### 为特定再现{#enable-xmp-writeback-for-specific-renditions}启用XMP回写

要让XMP回写功能将元数据更改传播到选择的演绎版，请将这些演绎版指定到DAM元数据回写工作流的[!UICONTROL XMP回写回进程]工作流步骤。 默认情况下，此步骤配置为原始再现。

要使XMP回写功能将元数据传播到再现缩略图140.100.png和319.319.png，请执行这些步骤。

1. 点按/单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模式]**。
1. 在“模型”页中，打开&#x200B;**[!UICONTROL DAM元数据写回]**&#x200B;工作流模型。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. 在&#x200B;**[!UICONTROL 步骤属性]**&#x200B;对话框中，点按/单击&#x200B;**[!UICONTROL 流程]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;框中，添加`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然后点按／单击&#x200B;**[!UICONTROL 确定]**。

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. 要使用新属性为 Dynamic Media 图像重新生成 Pyramid TIFF (PTIFF) 呈现，请将 **[!UICONTROL Dynamic Media 流程图像资产]**&#x200B;步骤添加到 DAM 元数据回写工作流。PTIFF 呈现仅在 Dynamic Media Hybrid 实施中本地创建和存储。

1. 保存工作流。

元数据更改将传播到资产的演绎版缩略图140.100.png和缩略图319.319.png，而不是其他演绎版。

>[!MORELIKETHIS]
>
>* [XMP规范(按Adobe)](https://www.adobe.com/devnet/xmp.html)

