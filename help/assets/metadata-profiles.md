---
title: 元数据配置文件
description: 了解资源的元数据配置文件。 了解如何创建元数据配置文件并将其应用于文件夹资产。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 21%

---

# 元数据配置文件 {#metadata-profiles}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service | 本文 |

元数据配置文件允许您将默认元数据应用到文件夹中的资源。 创建元数据配置文件并将其应用到文件夹。 您随后上传到文件夹的任何资产都会继承您在元数据配置文件中配置的默认元数据。

在Experience Manager Assets中使用用户档案的一个重要概念就是将其分配给文件夹。 在配置文件中，是元数据配置文件形式的设置，以及视频配置文件或图像配置文件。 这些设置处理文件夹及其任何子文件夹的内容。 因此，如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件对配置文件处理这些资产的方式有显着的影响。
通过使用一致且适用的文件和文件夹命名策略以及良好的元数据做法，您可以充分利用数字资产收藏集，并确保由正确的配置文件处理正确的文件。

## 添加元数据配置文件 {#adding-a-metadata-profile}

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据配置文件]**，然后单击&#x200B;**[!UICONTROL 创建]**。
1. 输入元数据配置文件的标题，例如示例元数据，然后选择&#x200B;**[!UICONTROL 提交]**。 此时将显示元数据配置文件的编辑表单。
1. 单击组件并在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中配置其属性。 例如，单击&#x200B;**[!UICONTROL Description]**组件并编辑其属性。
编辑**[!UICONTROL Description]**&#x200B;组件的以下属性：

   * **[!UICONTROL 字段标签]** — 元数据属性的显示名称。 仅供用户参考。
   * **[!UICONTROL 映射到属性]** — 此属性的值提供资产节点在存储库中保存的相对路径/名称。 该值应始终以`./`开头，因为它指示路径在资产的节点下。

     您为&#x200B;**[!UICONTROL 映射到属性]**&#x200B;指定的值作为属性存储在资产的元数据节点下。 例如，如果您指定`/jcr:content/metadata/dc:desc`作为&#x200B;**[!UICONTROL 映射到属性]**&#x200B;的名称，[!DNL Adobe Experience Manager Assets]将值`dc:desc`存储在资产的元数据节点。

   * **[!UICONTROL 默认值]** — 使用此属性为元数据组件添加默认值。 例如，如果您指定“我的描述”，则此值将分配给资产元数据节点上的属性`dc:desc`。

     >[!NOTE]
     >
     >默认情况下，向新元数据属性（不存在于`/jcr:content/metadata`节点中）添加默认值不会在资产的“属性”页面上显示该属性及其值。 要在[!UICONTROL 属性]页面上查看新属性，请修改相应的架构表单。

1. （可选）从“构建表单”选项卡中向“编辑表单”添 **[!UICONTROL 加更多组件]** ，然后在“设置”选项卡中配置 **[!UICONTROL 其属性]** 。 “构建表单”选项卡中提供 **[!UICONTROL 以下属性]** :

| 组件 | 属性 |
|------------------|----------------------------------------------------|
| 章节标题 | 字段标签，描述 |
| 单行文本 | 字段标签，映射到属性，默认值 |
| 多值文本 | 字段标签，映射到属性，默认值 |
| 数字 | 字段标签，映射到属性，默认值 |
| 日期 | 字段标签，映射到属性，默认值 |
| 标准标记 | 字段标签、映射到属性、默认值、描述 |

1. 单击&#x200B;**[!UICONTROL 完成]**。 元数据配置文件已添加到&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

## 复制元数据配置文件 {#copying-a-metadata-profile}

1. 从&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择一个元数据配置文件以制作其副本。
1. 单击工具栏中的&#x200B;**[!UICONTROL 复制]**。
1. 在&#x200B;**[!UICONTROL 复制元数据配置文件]**&#x200B;对话框中，输入元数据配置文件新副本的标题。
1. 单击&#x200B;**[!UICONTROL 复制]**。 元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

## 删除元数据配置文件 {#deleting-a-metadata-profile}

1. 从&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择要删除的配置文件。
1. 单击工具栏中的&#x200B;**[!UICONTROL 删除元数据配置文件]**。
1. 在对话框中，单击&#x200B;**[!UICONTROL 删除]**&#x200B;以确认删除操作。 元数据配置文件将从列表中删除。

## 将元数据配置文件应用到文件夹 {#applying-a-metadata-profile-to-folders}

将元数据配置文件分配给文件夹时，任何子文件夹都会自动从其父文件夹继承配置文件。 将其他配置文件应用于子文件夹时，继承将停止。 您只能将一个元数据配置文件分配给文件夹。 因此，请仔细考虑您上传、存储、使用和存档资产的文件夹结构。

如果为文件夹分配了不同的元数据配置文件，则新配置文件将覆盖以前的配置文件。 以前存在的文件夹资产保持不变。 新配置文件将应用于更改后添加到文件夹的资源。 您可以将元数据配置文件应用到特定文件夹，或全局应用到所有资源。

为其分配了配置文件的文件夹在用户界面中由卡片名称中显示的配置文件名称指示。

如果文件夹已具有您后来更改的现有元数据配置文件，您可以重新处理该文件夹中的资产。<!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 将元数据配置文件应用到特定文件夹 {#applying-metadata-profiles-to-specific-folders}

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

如果文件夹已具有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 将元数据配置文件从“配置文件”用户界面应用到文件夹 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 导航到&#x200B;**[!UICONTROL 工具> Assets >元数据配置文件]**。
1. 选择要应用于一个或多个文件夹的元数据配置文件。
1. 单击&#x200B;**[!UICONTROL 将元数据配置文件应用到文件夹]**，然后选择一个或多个用于接收新上传资源的文件夹，然后单击&#x200B;**[!UICONTROL 完成]**。 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 将元数据配置文件从“属性”应用到文件夹 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左边栏中，单击&#x200B;**[!UICONTROL Assets]**，然后导航到要将元数据配置文件应用到其中的文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择&#x200B;**属性**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，然后从下拉菜单中选择配置文件，然后单击&#x200B;**[!UICONTROL 保存]**。 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 全局应用元数据配置文件 {#applying-a-metadata-profile-globally}

除了将配置文件应用到文件夹外，您还可以全局应用配置文件，以便任何文件夹中上传到[!DNL Experience Manager Assets]的任何内容均已应用选定的配置文件。

如果文件夹已具有您后来更改的现有元数据配置文件，您可以重新处理该文件夹中的资产。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全局应用元数据配置文件，请执行下列操作之一**

* 导航到`https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam`并应用相应的配置文件，然后单击&#x200B;**[!UICONTROL 保存]**。

* 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`。 添加属性`metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`。 单击&#x200B;**全部保存**。

## 从文件夹中删除元数据配置文件 {#removing-a-metadata-profile-from-folders}

从文件夹中删除元数据配置文件时，所有子文件夹都会自动从其父文件夹中删除该配置文件。 但是，在文件夹中进行的任何文件处理操作将保持不变。

您可以从&#x200B;**工具**&#x200B;菜单中的文件夹删除元数据配置文件，或者如果您在文件夹中，也可以直接从&#x200B;**属性**&#x200B;中删除。本节将介绍如何通过这两种方式将元数据配置文件从文件夹中删除。

### 通过“配置文件”用户界面从文件夹中删除元数据配置文件 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 单击Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具> Assets >元数据配置文件]**。
1. 选择要从一个或多个文件夹中删除的元数据配置文件。
1. 单击&#x200B;**[!UICONTROL 从文件夹中删除元数据配置文件]**，然后选择一个或多个要从中删除配置文件的文件夹，然后单击&#x200B;**[!UICONTROL 完成]**。

   您可以确认元数据配置文件不再应用于文件夹，因为该名称不再出现在文件夹名称下方。

### 通过属性从文件夹中删除元数据配置文件 {#removing-metadata-profiles-from-folders-via-properties}

1. 单击Experience Manager徽标并导航&#x200B;**[!UICONTROL Assets]**，然后转到要删除元数据配置文件的文件夹。
1. 在文件夹上，单击复选标记将其选中，然后单击&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

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
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
