---
title: 配置Workfront和Experience Manager Assets之间的资源元数据映射
description: 在Adobe Workfront和Experience Manageras a Cloud Service的应用程序之间映射资源元数据字段。 作为映射元数据字段的结果，在将资源从Workfront发送到Experience Manager Assets时，您可以在Experience Manager Assets中查看映射的资源元数据。
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 4%

---

# 配置Adobe Workfront和Experience Manager Assets之间的资源元数据映射 {#asset-metadata-mapping-workfront-aem-assets}

您可以在Adobe Workfront与Experience Manageras a Cloud Service的应用程序之间映射资源元数据字段。 作为映射元数据字段的结果，在将资源从Workfront发送到Experience Manager Assets时，您可以在Experience Manager Assets中查看映射的资源元数据。

例如，在将图像发送到Experience Manager Assets时，如果您需要保留图像的元数据字段，例如名称、描述及其在Workfront中属于的项目，请配置这些字段并将其映射到Experience Manager Assets属性。

**用例**

图像 `add-users-workfront.png` 存在于 `Metadata Syncs` Adobe Workfront应用程序中的项目。 您需要将该图像与以下元数据发送到Experience Manager Assetsas a Cloud Service：

* 项目名称

* 文档名称

* 文档描述

## 前提条件 {#prerequisites}

* 拥有Workfront和Experience Manager Assetsas a Cloud Service应用程序的管理员访问权限。

* 之间的集成 [Workfront和Experience Manager Assetsas a Cloud Service应用程序](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## 在Workfront中设置元数据映射 {#set-up-metadata-mapping}

要在Workfront中设置项目名称、文档名称和文档描述字段的元数据映射，请执行以下操作：

1. 单击主菜单图标 ![显示菜单](assets/show-menu.svg) (位于Adobe Workfront应用程序的右上角)，然后单击 **[!UICONTROL 设置]**.

1. 选择 **[!UICONTROL 文档]** 在左侧面板中，然后选择 **[!UICONTROL Experience Manager Assets]**.

1. 选择Experience Manager Assets集成，然后单击 **[!UICONTROL 编辑]**.

1. 单击 **[!UICONTROL 元数据]**. 在 **[!UICONTROL 资产]** 选项卡，映射 [!UICONTROL 项目] > [!UICONTROL 名称] 的Workfront字段 `wm:projectName` Experience Manager Assets字段。 如果找不到完全匹配的项，Adobe建议查找用于映射Workfront和Experience Manager Assets字段的最佳匹配项。 您可以避免映射不同数据类型的字段。 例如，将日期Workfront字段映射到描述资源字段。
1. 映射 [!UICONTROL 文档] > [!UICONTROL 名称] 的Workfront字段 `wm:documentName` Experience Manager Assets字段。

   ![Workfront中的映射](assets/workfront-metadata-mapping.png)

1. 映射 [!UICONTROL 文档] > [!UICONTROL 描述] 的Workfront字段 `dc:description` Experience Manager Assets字段。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 将图像从Workfront发送到Experience Manager Assets {#send-image-workfront-assets}

要将图像从Workfront发送到Experience Manager Assets，请执行以下操作：

1. 单击主菜单图标 ![显示菜单](assets/show-menu.svg) (位于Adobe Workfront应用程序的右上角)，然后单击 **[!UICONTROL 项目]**.

1. 单击 **[!UICONTROL 新建项目]** 以创建项目。

1. 单击 **[!UICONTROL 文档]** 选项在左窗格中可用，拖动，然后选择要发送到Experience Manager Assets的图像。

1. 单击 **[!UICONTROL 发送至]**，然后选择Experience Manager Assets Essentials集成名称。

   ![发送到 AEM](assets/send-to-aem.png)

1. 选择资产的目标文件夹，然后单击 **[!UICONTROL 选择文件夹]**.

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 在Experience Manageras a Cloud Service中配置资源元数据映射 {#metadata-mapping-aem}

之后 [在Adobe Workfront中配置资源元数据映射](#set-up-metadata-mapping)中，您必须在Experience Manager Assetsas a Cloud Service应用程序中使用相同的映射，才能显示图像的相应元数据结果。

使用Experience Manager Assets中的元数据架构执行元数据映射。 您可以编辑新添加或现有的元数据架构表单。 元数据架构表单包括选项卡和选项卡中的表单项。 您可以将这些表单项映射/配置到CRX存储库中元数据节点内的字段。 您可以将选项卡或表单项添加到元数据架构表单。 有关更多信息，请参阅 [元数据架构](metadata-schemas.md).

要在Experience Manager Assetsas a Cloud Service中使用新的元数据表单配置元数据映射，请执行以下操作：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.

1. 单击 **[!UICONTROL 创建]** 工具栏中。 在对话框中，提供架构表单的标题，然后单击 **[!UICONTROL 创建]** 以完成表单创建过程。

1. 选择架构表单并单击 **[!UICONTROL 编辑]**.

1. （可选）在元数据架构表单编辑器中，单击 `+` 为Workfront字段创建选项卡。

1. 单击 **[!UICONTROL 构建表单]** 制表符并拖动 **[!UICONTROL 单行文本]** 组件添加到表单。 单击窗体中的组件。 在 **[!UICONTROL 构建表单]** 选项卡：

   1. 指定 `Project Name` 在 **[!UICONTROL 字段标签]** 字段。

   1. 指定 `./jcr:content/metadata/wm:projectName` 在 **[!UICONTROL 映射到属性]** 字段。 作为指导，请使用以下模板在Experience Manger Assets中定义字段映射：
      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront中配置映射时，您已映射 `wm:projectName` Experience Manager Assets字段到项目>命名Workfront字段。

      `wm` 是指命名空间名称和 `projectName` 是指属性标题。 使用 `namespace:propertyTitle` 定义元数据字段映射的格式。

      ![发送到 AEM](assets/metadata-schema-mapping.png)

1. 单击 **[!UICONTROL 构建表单]** 制表符并拖动 **[!UICONTROL 单行文本]** 组件添加到表单。 单击窗体中的组件。 在 **[!UICONTROL 构建表单]** 选项卡：

   1. 指定 `Document Name` 在 **[!UICONTROL 字段标签]** 字段。

   1. 指定 `./jcr:content/metadata/wm:documentName` 在 **[!UICONTROL 映射到属性]** 字段。
在Workfront中配置映射时，您已映射 `wm:documentName` Experience Manager Assets字段更改为文档>命名Workfront字段。

1. 单击 **[!UICONTROL 构建表单]** 制表符并拖动 **[!UICONTROL 多行文本]** 组件添加到表单。 单击窗体中的组件。 在 **[!UICONTROL 构建表单]** 选项卡：

   1. 指定 `Document Description` 在 **[!UICONTROL 字段标签]** 字段。

   1. 指定 `./jcr:content/metadata/dc:description` 在 **[!UICONTROL 映射到属性]** 字段。
在Workfront中配置映射时，您已映射 `dc:description` 将Experience Manager Assets字段更改为文档>描述Workfront字段。

1. 单击 **[!UICONTROL 保存]** 以保存更改。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 将元数据设置应用于图像文件夹 {#apply-metadata-settings-image-folder}

在Experience Manageras a Cloud Service应用程序中配置元数据设置后，将这些设置应用于 [包含从Workfront应用程序发送的图像的文件夹](#send-image-workfront-assets).

要将元数据设置应用到图像文件夹，请执行以下操作：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.

1. 从可用列表中选择元数据架构，然后单击 **[!UICONTROL 应用到文件夹]**.

1. 选择目标文件夹 [图像从Adobe Workfront应用程序发送](#send-image-workfront-assets) 并单击 **[!UICONTROL 应用]**.

您可以导航到Experience Manager Assets中的图像，并查看与图像关联的元数据。 选择图像并单击 **[!UICONTROL 属性]** 以查看图像元数据。

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
