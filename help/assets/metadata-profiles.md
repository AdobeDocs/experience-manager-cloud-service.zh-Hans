---
title: 元数据配置文件
description: 了解资产的元数据用户档案。 了解如何创建元数据用户档案并将其应用到文件夹资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 38%

---


# 元数据配置文件 {#metadata-profiles}

通过元数据用户档案，您可以将默认元数据应用到文件夹内的资产。 创建元数据用户档案并将其应用到文件夹。 您随后上传到文件夹的任何资产都会继承您在元数据用户档案中配置的默认元数据。

<!-- See [Profiles for Processing Metadata, Images, and Videos](processing-profiles.md).

See also [Best Practices for Organizing your Digital Assets for using Processing Profiles](/help/assets/best-practices-for-file-management.md).

-->

## 添加元数据用户档案 {#adding-a-metadata-profile}

1. 点按AEM徽标，然后导航到 **[!UICONTROL 工具>资产>元数据用户档案]**，然后点按 **[!UICONTROL 创建]**。
1. 为元数据用户档案（例如示例元数据）输入标题，然后点按 **[!UICONTROL 提交]**。 此时将显示元数据用户档案的编辑表单。
1. Click a component and configure its properties in the **[!UICONTROL Settings]** tab. For example, click the **[!UICONTROL Description]** component and edit its properties.
Edit the following properties for the **[!UICONTROL Description]** component:

   * **[!UICONTROL 字段标签]** -元数据属性的显示名称。 仅供用户参考。
   * **[!UICONTROL 映射到属性]** -此属性的值提供资产节点在存储库中保存的相对路径／名称。 该值应始终与开始 `./` ，因为它指示该路径位于资产的节点下。

      您为&#x200B;**[!UICONTROL 映射到属性]**&#x200B;指定的值会作为属性存储在资产的元数据节点下。例如，如果您指定`/jcr:content/metadata/dc:desc` 作为映射到属 **[!UICONTROL 性的名称]**,AEM资产会将该值存储 `dc:desc` 在资产的元数据节点。

   * **[!UICONTROL 默认值]** -使用此属性为元数据组件添加默认值。 For example, if you specify &quot;My description&quot; then this value is assigned to the property `dc:desc` at the asset&#39;s metadata node.

      >[!NOTE]
      >
      >向新元数据属性添加默认值（在中尚不存在）。 `/jcr:content/metadata` 节点)默认情况下不在资产的“属性”页面上显示属性及其值。 要视图资产的“属性”页面上的新属性，请修改相应的模式表单。

1. （可选）从“构建表单”选项卡中向“编辑表单”添 **[!UICONTROL 加更多组件]** ，然后在“设置”选项卡中配置 **[!UICONTROL 其属性]** 。 “构建表单”选项卡中提供 **[!UICONTROL 以下属性]** :

| 组件 | 属性 |
|------------------|----------------------------------------------------|
| 章节标题 | 字段标签，说明 |
| 单行文本 | 字段标签、映射到属性、默认值 |
| 多值文本 | 字段标签、映射到属性、默认值 |
| 数字 | 字段标签、映射到属性、默认值 |
| 日期 | 字段标签、映射到属性、默认值 |
| 标准标记 | 字段标签、映射到属性、默认值、说明 |

1. 点按&#x200B;**[!UICONTROL 完成]**。The Metadata Profile is added to the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

## 复制元数据用户档案 {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a Metadata Profile to make a copy of it.
1. 从工 **[!UICONTROL 具栏]** 中点按复制。
1. 在&#x200B;**[!UICONTROL 复制元数据配置文件]**&#x200B;对话框中，为元数据配置文件的新副本输入标题。
1. 点按&#x200B;**[!UICONTROL 复制]**。元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

## 删除元数据用户档案 {#deleting-a-metadata-profile}

1. 在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择要删除的配置文件。
1. 点按 **[!UICONTROL 工具栏中的]** “删除元数据”用户档案。
1. In the dialog, click **[!UICONTROL Delete]** to confirm the delete operation. The metadata profile is deleted from the list.

## Apply a metadata profile to folders {#applying-a-metadata-profile-to-folders}

当您将元数据配置文件分配给文件夹之后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。这就意味着您只能为每个文件夹分配一个元数据配置文件。因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果您为文件夹分配了一个不同的元数据配置文件，新配置文件就会取代之前的配置文件。此前存在的文件夹资产将保持不变。新用户档案将应用于稍后添加到该文件夹的资产。

在用户界面中，卡名称中显示的用户档案名称会指示已为其分配用户档案的文件夹。

您可以将元数据用户档案应用于特定文件夹或全局应用于所有资产。

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 将元数据用户档案应用于特定文件夹 {#applying-metadata-profiles-to-specific-folders}

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

You can reprocess assets in a folder that already has an existing video profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Apply metadata profiles to folders from Profiles user interface {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 选择您要应用到一个或多个文件夹的元数据配置文件。
1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 从“属性”将元数据用户档案应用到文件夹 {#applying-metadata-profiles-to-folders-from-properties}

1. In the left rail, tap **[!UICONTROL Assets]** then navigate to the folder that you want to apply a metadata profile to.
1. 在文件夹中，点按或单击复选标记以将其选中，然后点按或单击 **属性**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，然后从下拉菜单中选择配置文件，然后点按&#x200B;**保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 全局应用元数据用户档案 {#applying-a-metadata-profile-globally}

除了将用户档案应用到文件夹外，您还可以全局应用一个用户档案，以便上传到任何文件夹中的AEM资产的任何内容都已应用选定的。

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**要全局应用元数据用户档案，请执行下列操作之一**

* 导航到 `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 并应用相应的用户档案，然后点 **按保存**。

* 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`. 添加属性， `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` 然后点 **按全部保存**。

## Removing a metadata profile from folders {#removing-a-metadata-profile-from-folders}

当您将元数据配置文件从文件夹删除之后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。但是，此前对文件夹中的文件所做的处理均予以保留。

您可以从&#x200B;**工具**&#x200B;菜单中的文件夹删除元数据配置文件，或者如果您在文件夹中，也可以直接从&#x200B;**属性**&#x200B;中删除。本节将介绍如何通过这两种方式将元数据配置文件从文件夹中删除。

### Removing metadata profiles from folders via Profiles user interface {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 点按或单击AEM徽标，然后导航到 **[!UICONTROL 工具>资产>元数据用户档案]**。
1. 选择您要从一个或多个文件夹删除的元数据配置文件。
1. 点按&#x200B;**[!UICONTROL 从文件夹删除元数据配置文件]**，然后选择一个或多个要从中删除配置文件的文件夹，然后点按&#x200B;**[!UICONTROL 完成]**。

   您可以确认元数据用户档案不再应用于文件夹，因为该名称不再显示在文件夹名称的下方。

### 通过属性从文件夹删除元数据用户档案 {#removing-metadata-profiles-from-folders-via-properties}

1. 点按AEM徽标，导 **[!UICONTROL 航资产]** ，然后导航到您要从中删除元数据用户档案的文件夹。
1. 在文件夹中，点按复选标记以将其选中，然后点按 **[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
