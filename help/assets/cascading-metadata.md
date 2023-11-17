---
title: 层叠元数据
description: 本文介绍了如何定义资源的层叠元数据。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 15%

---

# 级联元数据 {#cascading-metadata}

在捕获资源的元数据信息时，用户在各种可用字段中提供信息。 您可以根据在其他字段中选择的选项，显示特定的元数据字段或字段值。 此类元数据的条件显示称为层叠元数据。 换言之，您可以在特定元数据字段/值与一个或多个字段和/或其值之间创建依赖关系。

使用元数据架构定义用于显示层叠元数据的规则。 例如，如果您的元数据架构包含资产类型字段，则可以根据用户选择的资产类型定义要显示的相关字段集。

以下是您可以定义层叠元数据的一些用例：

* 在需要用户位置时，根据用户选择的国家和州显示相关城市名称。
* 根据用户选择的产品类别，在列表中加载相关品牌名称。
* 根据在另一个字段中指定的值切换特定字段的可见性。 例如，如果用户希望以不同的地址交付装运，则显示单独的装运地址字段。
* 根据在另一个字段中指定的值将某个字段指定为必填字段。
* 根据在另一个字段中指定的值更改为特定字段显示的选项。
* 根据在其他字段中指定的值在特定字段中设置默认元数据值。

## 在中配置层叠元数据 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

考虑一个方案，其中您要根据所选资源的类型显示层叠元数据。 一些示例

* 对于视频，显示适用的字段，例如格式、编解码器、持续时间等。
* 对于Word或PDF文档，显示字段，例如页数、作者等。

无论选择的资产类型如何，都会将版权信息显示为必填字段。

1. 点按/单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 在&#x200B;**[!UICONTROL 架构表单]**&#x200B;页面中，选择一个架构表单，然后点按/单击工具栏中的&#x200B;**[!UICONTROL 编辑]**，以编辑架构。

   ![select_form](assets/select_form.png)

1. （可选）在元数据架构编辑器中，创建一个要条件化的字段。 在中指定名称和属性路径 **[!UICONTROL 设置]** 选项卡。

   要创建选项卡，请点按/单击 `+` 以添加选项卡，然后添加元数据字段。

   ![add_tab](assets/add_tab.png)

1. 为资源类型添加下拉字段。 在中指定名称和属性路径 **[!UICONTROL 设置]** 选项卡。 添加可选描述。

   ![asset_type_field](assets/asset_type_field.png)

1. 键值对是提供给表单用户的选项。 您可以手动或从JSON文件提供键值对。

   * 要手动指定值，请选择 **[!UICONTROL 手动添加]**，然后点按/单击 **[!UICONTROL 添加选项]** 并指定选项文本和值。 例如，指定视频、PDF、Word和图像资源类型。

   * 要动态获取JSON文件中的值，请选择 **[!UICONTROL 通过JSON路径添加]** 和提供JSON文件的路径。 [!DNL Experience Manager] 向用户呈现表单时实时获取键值对。

   两个选项是互斥的。 您无法从JSON文件导入选项并手动编辑。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >添加JSON文件时，键值对不会显示在元数据架构编辑器中，但可在发布的表单中使用。

   >[!NOTE]
   >
   >添加选项时，如果单击弹出式字段，界面将扭曲，且选项的删除图标将停止工作。 在保存更改之前，请勿单击下拉列表。 如果您遇到此问题，请保存架构并再次打开它以继续编辑。

1. （可选）添加其他必填字段。 例如，资源类型视频的格式、编解码器和持续时间。

   同样，为其他资源类型添加依赖字段。 例如，为文档资源(如PDF和Word文件)添加字段页数和作者。

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 要在资产类型字段和其他字段之间创建依赖关系，请选择依赖字段并打开 **[!UICONTROL 规则]** 选项卡。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 下 **[!UICONTROL 要求]**，选择 **[!UICONTROL 必需，基于新规则]** 选项。
1. 点按／单 **[!UICONTROL 击添加规则]** ，然后选择“资 **[!UICONTROL 产类型]** ”字段以创建依赖关系。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 点按／单击 **[!UICONTROL 完成]** ，以保存更改。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >带有手动预定义值的下拉列表可与规则一起使用。 已配置JSON路径的下拉菜单无法与使用预定义值来应用条件的规则一起使用。 如果在运行时从JSON加载值，则无法应用预定义规则。

1. 在“可 **[!UICONTROL 见性]**”下，根据新 **[!UICONTROL 规则选项选择“可见]** ”。

1. 点按／单 **[!UICONTROL 击添加规则]** ，然后选择“资 **[!UICONTROL 产类型]** ”字段以创建依赖关系。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 点按／单击 **[!UICONTROL 完成]** ，以保存更改。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >要重置值，请单击或点按空白或界面上除值之外的任何其他位置。 如果重置了值，请再次选择值。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

1. 同样，在资产类型字段中的值Video与其他字段（例如，编解码器和持续时间）之间创建依赖关系。
1. 重复这些步骤以在中的文档资源(PDF和Word)之间创建依赖关系 [!UICONTROL 资源类型] 字段和字段，例如 [!UICONTROL 页数] 和 [!UICONTROL 作者].
1. 单击&#x200B;**[!UICONTROL 保存]**。将元数据架构应用到文件夹。

1. 导航到将元数据架构应用到的文件夹，然后打开资源的属性页面。 根据您在“资产类型”字段中的选择，将显示相关的级联元数据字段。

   ![视频资源的级联元数据](assets/video_asset.png)
   *图：视频资源的层叠元数据*

   ![文档资产的级联元数据](assets/doc_type_fields.png)
   *图：文档资源的层叠元数据*

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
