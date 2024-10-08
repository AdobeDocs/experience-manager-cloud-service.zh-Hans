---
title: 配置Workfront和Experience Manager Assets之间的资源元数据映射
description: 在Adobe Workfront和Experience Manager元数据应用程序之间映射as a Cloud Service资源字段。 作为映射元数据字段的结果，在将资源从Workfront发送到Experience Manager Assets时，您可以在Experience Manager Assets中查看映射的资源元数据。
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
feature: Metadata, Workfront Integrations and Apps
role: User, Admin
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 4%

---

# 配置Adobe Workfront和Experience Manager Assets之间的资源元数据映射 {#asset-metadata-mapping-workfront-aem-assets}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

您可以在Adobe Workfront和Experience Manager元数据应用程序之间映射as a Cloud Service资源字段。 作为映射元数据字段的结果，在将资源从Workfront发送到Experience Manager Assets时，您可以在Experience Manager Assets中查看映射的资源元数据。

例如，在将图像发送到Experience Manager Assets时，如果您需要保留图像的元数据字段，例如名称、描述及其在Workfront中属于的项目，请配置这些字段并将其映射到Experience Manager Assets属性。

**用例**

Adobe Workfront应用程序的`Metadata Syncs`项目中存在图像`add-users-workfront.png`。 您需要将该图像与以下元数据发送到Experience Manager Assetsas a Cloud Service：

* 项目名称

* 文档名称

* 文档描述

## 先决条件 {#prerequisites}

* 拥有Workfront和Experience Manager Assetsas a Cloud Service应用程序的管理员访问权限。

* [Workfront与Experience Manager Assetsas a Cloud Service应用程序](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus)之间的集成。

## 在Workfront中设置元数据映射 {#set-up-metadata-mapping}

要在Workfront中设置项目名称、文档名称和文档描述字段的元数据映射，请执行以下操作：

1. 单击Adobe Workfront应用程序右上角可用的主菜单图标![显示菜单](assets/show-menu.svg)，然后单击&#x200B;**[!UICONTROL 设置]**。

1. 在左侧面板中选择&#x200B;**[!UICONTROL 文档]**，然后选择&#x200B;**[!UICONTROL Experience Manager Assets]**。

1. 选择Experience Manager Assets集成，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 单击&#x200B;**[!UICONTROL 元数据]**。 在&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡中，将[!UICONTROL Project] > [!UICONTROL Name] Workfront字段映射到`wm:projectName` Experience Manager Assets字段。 如果找不到完全匹配的项，Adobe建议您查找用于映射Workfront和Experience Manager Assets字段的最佳匹配项。 您可以避免映射不同数据类型的字段。 例如，将日期Workfront字段映射到描述Assets字段。
1. 将[!UICONTROL Document] > [!UICONTROL Name] Workfront字段映射到`wm:documentName` Experience Manager Assets字段。

   Workfront中的![映射](assets/workfront-metadata-mapping.png)

1. 将[!UICONTROL Document] > [!UICONTROL Description] Workfront字段映射到`dc:description` Experience Manager Assets字段。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 将图像从Workfront发送到Experience Manager Assets {#send-image-workfront-assets}

要将图像从Workfront发送到Experience Manager Assets，请执行以下操作：

1. 单击Adobe Workfront应用程序右上角可用的主菜单图标![显示菜单](assets/show-menu.svg)，然后单击&#x200B;**[!UICONTROL 项目]**。

1. 单击&#x200B;**[!UICONTROL 新建项目]**&#x200B;以创建项目。

1. 单击左窗格中可用的&#x200B;**[!UICONTROL 文档]**&#x200B;选项，拖动，然后选择要发送到Experience Manager Assets的图像。

1. 单击&#x200B;**[!UICONTROL 发送至]**，然后选择Experience Manager Assets Essentials集成名称。

   ![发送至AEM](assets/send-to-aem.png)

1. 选择资产的目标文件夹，然后单击&#x200B;**[!UICONTROL 选择文件夹]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 在Experience Manageras a Cloud Service中配置资源元数据映射 {#metadata-mapping-aem}

在[在Adobe Workfront](#set-up-metadata-mapping)中配置资源元数据映射后，您必须在Experience Manager Assetsas a Cloud Service应用程序中使用相同的映射来显示该图像的相应元数据结果。

使用Experience Manager Assets中的元数据架构执行元数据映射。 您可以编辑新添加或现有的元数据架构表单。 元数据架构表单包括选项卡和选项卡中的表单项。 您可以将这些表单项目映射/配置到CRX存储库中元数据节点内的字段。 您可以将选项卡或表单项添加到元数据架构表单。 有关详细信息，请参阅[元数据架构](metadata-schemas.md)。

要在Experience Manager Assetsas a Cloud Service中使用新的元数据表单配置元数据映射，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。

1. 单击工具栏中的&#x200B;**[!UICONTROL 创建]**。 在对话框中，提供架构表单的标题，然后单击&#x200B;**[!UICONTROL 创建]**&#x200B;以完成表单创建过程。

1. 选择架构表单并单击&#x200B;**[!UICONTROL 编辑]**。

1. （可选）在元数据架构表单编辑器中，单击`+`以创建Workfront字段的选项卡。

1. 单击&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡，并将&#x200B;**[!UICONTROL 单行文本]**&#x200B;组件拖到表单中。 单击窗体中的组件。 在&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡中：

   1. 在&#x200B;**[!UICONTROL 字段标签]**&#x200B;字段中指定`Project Name`。

   1. 在&#x200B;**[!UICONTROL 映射到属性]**&#x200B;字段中指定`./jcr:content/metadata/wm:projectName`。 作为指导，请使用以下模板在Experience Manger Assets中定义字段映射：
      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront中配置映射时，您已将`wm:projectName`个Experience Manager Assets字段映射到项目>命名Workfront字段。

      `wm`引用命名空间名称，`projectName`引用属性标题。 使用`namespace:propertyTitle`格式定义元数据字段映射。

      ![发送至AEM](assets/metadata-schema-mapping.png)

1. 单击&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡，并将&#x200B;**[!UICONTROL 单行文本]**&#x200B;组件拖到表单中。 单击窗体中的组件。 在&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡中：

   1. 在&#x200B;**[!UICONTROL 字段标签]**&#x200B;字段中指定`Document Name`。

   1. 在&#x200B;**[!UICONTROL 映射到属性]**&#x200B;字段中指定`./jcr:content/metadata/wm:documentName`。
在Workfront中配置映射时，您已将`wm:documentName`个Experience Manager Assets字段映射到文档>命名Workfront字段。

1. 单击&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡，并将&#x200B;**[!UICONTROL 多行文本]**&#x200B;组件拖到表单中。 单击窗体中的组件。 在&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡中：

   1. 在&#x200B;**[!UICONTROL 字段标签]**&#x200B;字段中指定`Document Description`。

   1. 在&#x200B;**[!UICONTROL 映射到属性]**&#x200B;字段中指定`./jcr:content/metadata/dc:description`。
在Workfront中配置映射时，您已将`dc:description`个Experience Manager Assets字段映射到文档>描述Workfront字段。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 将元数据设置应用于图像文件夹 {#apply-metadata-settings-image-folder}

在Experience Manageras a Cloud Service应用程序中配置元数据设置后，将这些设置应用到包含从Workfront应用程序](#send-image-workfront-assets)发送的图像的[文件夹。

要将元数据设置应用到图像文件夹，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。

1. 从可用列表中选择元数据架构，然后单击&#x200B;**[!UICONTROL 应用到文件夹]**。

1. 选择[从Adobe Workfront应用程序](#send-image-workfront-assets)将图像发送到的目标文件夹&#x200B;**[!UICONTROL 应用]**。

您可以导航到Experience Manager Assets中的图像，并查看与图像关联的元数据。 选择图像并单击&#x200B;**[!UICONTROL 属性]**&#x200B;以查看图像元数据。

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
