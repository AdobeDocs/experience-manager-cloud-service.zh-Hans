---
title: XMP元数据
description: 了解用于元数据管理的XMP（可扩展元数据平台）元数据标准。 AEM将其用作创建、处理和交换元数据的标准格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# XMP metadata {#xmp-metadata}

XMP（可扩展元数据平台）是 AEM 资产用来进行所有元数据管理的元数据标准。XMP 为在各种应用程序中创建、处理和交换元数据提供了一种标准格式。

Aside from offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich [content model](#xmp-core-concepts) and is [supported by Adobe](#advantages-of-xmp) and other companies, so that users of XMP in combination with AEM Assets have a powerful platform to build upon.

## XMP概述和生态系统 {#xmp-ecosystem}

AEM资产本机支持XMP元数据标准。 XMP是处理和存储数字资产中标准化的专有元数据的标准。 XMP 旨在形成通用标准，从而让多个应用程序能够高效地处理元数据。

例如，专业生产人士可以使用 Adobe 应用程序中内置的 XMP 支持，在多种文件格式之间传递信息。AEM 资产存储库会提取 XMP 元数据，用它来管理内容生命周期，并提供创建自动化工作流的能力。

XMP 通过提供数据模型、存储模型和架构，使元数据的定义、创建和处理方式实现标准化。本节将介绍所有这些概念。

来自 EXIF、ID3 或 Microsoft Office 的所有旧版元数据都将自动转换为 XMP，而 XMP 可进行扩展，以支持特定于客户的元数据架构，例如产品目录。

XMP 中的元数据包含一组属性。这些属性始终与称为资源的特定实体相关联；即，属性是“关于”资源的。 对于 XMP，资源始终是指资产。

XMP 定义了一个[元数据](https://en.wikipedia.org/wiki/Metadata)模型，该模型可与任何定义的元数据项目集结合使用。XMP 还为基本属性定义了特定[架构](https://en.wikipedia.org/wiki/XML_schema)，这些属性用于记录资源经过多个处理步骤的历史，包括从拍摄、[扫描](https://en.wikipedia.org/wiki/Image_scanner)或配文字，到照片编辑步骤（例如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到整合成最终的图像。XMP 允许每个软件程序或设备在处理过程中向数字资源添加自己的信息，然后可在最终的数字文件中保留这些信息。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 进行序列化和存储，而 RDF 又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP 的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP 具有以下优势：

* 基于 XMP 的元数据非常强大且精细。
* XMP 允许您为一个属性设置多个值。
* XMP 采用标准化的编码，让您可以轻松交换元数据。
* XMP 具有可扩展性。您可以向资产中添加其他信息。

XMP标准设计为可扩展，允许您向XMP数据中添加自定义类型的元数据。 而EXIF则不然——它有一个无法扩展的属性的修正列表。

>[!NOTE]
>
>XMP 一般不允许嵌入二进制类型的数据。To carry binary data in XMP, for example, thumbnail images, they must be encoded in an XML-friendly format such as `Base64`.

### XMP core concepts {#xmp-core-concepts}

**命名空间和架构**

XMP 架构是通用 XML 命名空间中的一组属性名称，包括数据类型和描述性信息。
XMP 架构采用其 XML 命名空间 URI 进行标识。使用命名空间可以防止不同架构内名称相同但含义不同的属性之间发生冲突。

例如，在两个独立设计的架构中，**创建者**&#x200B;属性可能指创建资产的人，也可能指创建资产的应用程序（例如，Adobe Photoshop）。

**XMP属性和值**

XMP 可以包含来自一个或多个架构的属性。例如，很多 Adobe 应用程序使用的典型子集包括以下架构：

* 都柏林核心架构： `dc:title`, `dc:creator``dc:subject`, `dc:format`, `dc:rights`
* XMP基本架构： `xmp:CreateDate`, `xmp:CreatorTool``xmp:ModifyDate`, `xmp:metadataDate`
* XMP权限管理架构： `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP media management schema: `xmpMM:DocumentID`

**替代语言**

XMP 支持向文本属性添加 `xml:lang` 属性以指定文本的语言。

## XMP 写回到演绎版 {#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)资产中的此XMP回写功能可将资产元数据更改复制到资产的演绎版。

当您从AEM资产中更改资产的元数据或在上传资产时，更改最初存储在CRXDE的资产节点中。

XMP回写功能可将元数据更改传播到资产的所有或特定演绎版。

请考虑将资产标题的 [!UICONTROL 标题] 属性修改为的 `Classic Leather` 场景 `Nylon`。

![元数据](assets/metadata.png)

In this case, the AEM Assets saves the changes to the **[!UICONTROL Title]** property in the `dc:title` parameter for the asset metadata stored in the asset hierarchy.

![metadata_stored](assets/metadata_stored.png)

但是，AEM资产不会自动将任何元数据更改传播到资产的演绎版。

XMP回写功能允许您将元数据更改传播到资产的所有或特定演绎版。 但是，这些更改不会存储在资产层次结构中的元数据节点下。此功能而是会将更改嵌入到演绎版的二进制文件中。

### 启用XMP回写 {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

要在上传元数据更改时将其传播到资产的演绎版，请在配置管理器中修改 **[!UICONTROL Adobe CQ DAM Rendition Maker]** 配置。

1. 要打开配置管理器，请访问 `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开 **[!UICONTROL Adobe CQ DAM Rendition Maker配置]** 。
1. 选择“ **[!UICONTROL 传播XMP]** ”选项，然后保存更改。

### 为特定再现启用XMP回写 {#enable-xmp-writeback-for-specific-renditions}

要让XMP回写功能将元数据更改传播到选定的演绎版，请将这些演绎版指定到DAM元数据回写工作流的  XMP回写流程工作流步骤。 默认情况下，此步骤配置有原始再现。

要使XMP回写功能将元数据传播到再现缩略图140.100.png和319.319.png，请执行这些步骤。

1. 点按／单击AEM徽标，然后导航到工具 **** >工作 **[!UICONTROL 流]** >模 **[!UICONTROL 型]**。
1. 从“模型”页面，打开 **[!UICONTROL DAM元数据写回工作流模型]** 。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. 在“步 **[!UICONTROL 骤属性]** ”对话框中，点按／单击“ **[!UICONTROL 进程]** ”选项卡。
1. 在“参 **[!UICONTROL 数]** ”框中，添加 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然后点按／单击 **[!UICONTROL 确定]**。

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. 要使用新属性为Dynamic media图像重新生成金字塔TIFF(PTIFF)再现，请将 **** Dynamic Media Process图像资产步骤添加到DAM元数据回写工作流。 PTIFF再现仅在Dynamic Media Hybrid实施中本地创建和存储。

1. 保存工作流。

元数据更改将传播到资产的演绎版thumbnail.140.100.png和thumbnail.319.319.png，而不是其他演绎版。

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### 过滤XMP元数据 {#filtering-xmp-metadata}

AEM资产支持对从资产二进制文件读取的、在摄取资产时存储在JCR中的XMP元数据的属性／节点进行黑名单和白名单过滤。

黑名单过滤允许您导入除为排除而指定的属性外的所有XMP元数据属性。 但是，对于具有大量XMP元数据（例如，1000个节点具有10,000个属性）的资产类型（如INDD文件），要筛选的节点名称并不总是预先知道的。 如果黑名单过滤允许导入大量具有大量XMP元数据的资产，则AEM实例／群集可能会遇到稳定性问题，例如，阻塞的观察队列。

XMP元数据的白名单过滤功能可通过允许您定义要导入的XMP属性来解决此问题。 这样，将忽略其他／未知的XMP属性。 您可以将其中一些属性添加到黑名单过滤器，以实现向后兼容性。

>[!NOTE]
>
>筛选仅适用于从资产二进制文件中的XMP源派生的属性。 对于从非XMP源（如EXIF和IPTC格式）派生的属性，过滤不起作用。 例如，资产创建日期存储在以EXIF TIFF命名的 `CreateDate` 属性中。 AEM在名为的元数据字段中讲述此值 `exif:DateTimeOriginal`。 由于源是非XMP源，因此过滤不适用于此属性。

1. 要打开配置管理器，请访问 `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开 **[!UICONTROL Adobe CQ DAM XmpFilter配置]** 。
1. 要应用白名单过滤，请选 **[!UICONTROL 择“将白名单应用于XMP属性”]**，然后在“XMP过滤的白名单XML名称”框中指定要导 **[!UICONTROL 入的属性]** 。

1. 要在应用白名单过滤后过滤掉列入黑名单的XMP属性，请在“XMP过滤的列入黑 **[!UICONTROL 名单的XML名称”框中指定]** 。

   >[!NOTE]
   >
   >默认 **[!UICONTROL 情况下，“将黑名单应用到XMP属性]** ”选项处于选中状态。 换句话说，黑名单过滤默认为启用状态。 要禁用黑名单过滤，请取消选择“将黑 **[!UICONTROL 名单应用到XMP属性]** ”选项。

1. 保存更改。

>[!MORELIKETHIS]
>
>* [Adobe的XMP规范](https://www.adobe.com/devnet/xmp.html)