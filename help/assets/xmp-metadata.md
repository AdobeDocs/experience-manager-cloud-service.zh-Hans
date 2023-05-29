---
title: XMP 元数据
description: 了解用于元数据管理的XMP（可扩展元数据平台）元数据标准。 它被Experience Manager用作创建、处理和交换元数据的标准化格式。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 18%

---

# XMP 元数据 {#xmp-metadata}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| AEM as a Cloud Service | 本文 |

XMP（可扩展元数据平台）是Experience Manager Assets用于所有元数据管理的元数据标准。 XMP为各种应用程序的元数据的创建、处理和交换提供了一个标准格式。

除了提供可以嵌入到所有文件格式的通用元数据编码之外，XMP还提供丰富的 [内容模型](#xmp-core-concepts) 和 [受Adobe支持](#advantages-of-xmp) 和其他公司，以便XMP的用户能够与 [!DNL Assets] 拥有强大的平台进行构建。

## XMP概述和生态系统 {#xmp-ecosystem}

[!DNL Assets] 原生支持XMP元数据标准。 XMP是在数字资产中处理和存储标准化的专有元数据的标准。 XMP旨在作为允许多个应用程序有效地使用元数据的通用标准。

例如，生产专业人员可以使用Adobe应用程序中内置的XMP支持，跨多种文件格式传递信息。 此 [!DNL Assets] 存储库提取XMP元数据并使用它来管理内容生命周期，并提供创建自动化工作流的功能。

XMP通过提供数据模型、存储模型和架构，实现了元数据的定义、创建和处理的标准化。 本节将介绍所有这些概念。

来自EXIF、ID3或Microsoft Office的所有旧元数据会自动转换为XMP，该架构可以扩展为支持客户特定的元数据架构，例如产品目录。

XMP中的元数据由一组属性组成。 这些属性始终与称为资源的特定实体相关联；即，这些属性是有关资源的。 对于XMP，资源始终是资源。

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP具有以下优势：

* 基于XMP的元数据功能非常强大且粒度非常细。
* XMP允许您为一个属性使用多个值。
* XMP具有标准化的编码，这使您能够轻松交换元数据。
* XMP可扩展。 您可以将其他信息添加到资源中。

XMP标准设计为可扩展，允许您向XMP数据添加自定义类型的元数据。 而EXIF则否 — 它有一个无法扩展的固定属性列表。

>[!NOTE]
>
>XMP通常不允许嵌入二进制数据类型。 要在XMP中携带二进制数据（例如缩略图图像），必须以XML友好格式对其进行编码，例如 `Base64`.

### XMP核心概念 {#xmp-core-concepts}

**命名空间和架构**

XMP架构是公共XML命名空间中的一组属性名称，其中包括数据类型和描述性信息。 XMP架构由其XML命名空间URI标识。 使用命名空间可防止不同架构中具有相同名称但不同含义的属性之间发生冲突。

例如， **创建者** 两个独立设计的架构中的资产可能是指创建资产的人，也可能是指创建资产的应用程序(例如，Adobe Photoshop)。

**XMP属性和值**

XMP可以包含一个或多个架构的属性。 例如，许多Adobe应用程序使用的典型子集可能包括：

* 都柏林核心模式： `dc:title`， `dc:creator`， `dc:subject`， `dc:format`， `dc:rights`
* XMP基本架构： `xmp:CreateDate`， `xmp:CreatorTool`， `xmp:ModifyDate`， `xmp:metadataDate`
* XMP权限管理架构： `xmpRights:WebStatement`， `xmpRights:Marked`
* XMP媒体管理模式： `xmpMM:DocumentID`

**替代语言**

XMP使您能够添加 `xml:lang` 属性到文本属性以指定文本的语言。

## XMP写回到演绎版 {#xmp-writeback-to-renditions}

中的此XMP写回功能 [!DNL Adobe Experience Manager Assets] 将元数据更改复制到原始资源的演绎版。
从中更改资源的元数据时 [!DNL Assets] 或者，在上传资源时，最初将更改存储在资源层次结构的元数据节点中。 回写功能允许您将元数据更改传播到资源的所有或特定演绎版。 该功能仅回写那些使用的元数据属性 `jcr` namespace，即名为的属性 `dc:title` 写回，但有一个名为 `mytitle` 不是。

例如，考虑一个方案，其中您修改了 [!UICONTROL 标题] 标题为的资产属性 `Classic Leather` 到 `Nylon`.

![元数据](assets/metadata.png)

在这个案例中， [!DNL Assets] 将更改保存到 **[!UICONTROL 标题]** 中的属性 `dc:title` 资源层次结构中存储的资源元数据的参数。

![元数据存储在存储库的资源节点中](assets/metadata_stored.png)

>[!IMPORTANT]
>
>默认情况下，中的回写功能未启用 [!DNL Assets]. 了解如何 [启用元数据写回](#enable-xmp-writeback). MSM for digital assets不适用于启用了元数据写回的情况。 在写回时，继承中断。

### 启用XMP写回 {#enable-xmp-writeback}

[!UICONTROL DAM元数据写回] 工作流用于写回资源的元数据。 要启用写回，请遵循以下三种方法之一：

* 使用启动器。
* 手动启动 `DAM MetaData Writeback` 工作流。
* 将工作流配置为后处理的一部分。

要使用启动器，请执行以下步骤：

1. 作为管理员，访问 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**.
1. 选择 [!UICONTROL 启动器] 对于 **[!UICONTROL 工作流]** 列显示 **[!UICONTROL DAM元数据写回]**. 单击 **[!UICONTROL 属性]** 工具栏中。

   ![选择DAM元数据写回启动器以修改其属性并激活它](assets/launcher-properties-metadata-writeback1.png)

1. 选择 **[!UICONTROL 激活]** 在 **[!UICONTROL 启动器属性]** 页面。 单击“**[!UICONTROL 保存并关闭]**”。

要仅将工作流手动应用于资产一次，请应用 [!UICONTROL DAM元数据写回] 工作流中的左边栏。

要将工作流应用于所有上传的资产，请将该工作流添加到后处理配置文件。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
