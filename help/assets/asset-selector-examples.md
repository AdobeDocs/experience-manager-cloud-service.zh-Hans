---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资产选择器根据需要进行自定义的示例。
role: Admin, User
exl-id: 7a393a96-f2a2-4a25-922c-577271cafc57
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 49%

---

# 有关使用资源选择器属性的示例 {#usage-examples}

您可以在&#x200B;**index.html**&#x200B;文件中定义资产选择器[属性](/help/assets/asset-selector-properties.md)，以自定义应用程序中的资产选择器显示。

## 示例 1：边栏视图中的资源选择器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果AssetSelector `rail`的值设置为`false`或未在属性中提及，则默认情况下，Asset Selector会显示在模式视图中。 `acvConfig`属性允许进行一些深入配置，如拖放。 访问[启用或禁用拖放](asset-selector-customization.md#enable-disable-drag-and-drop)以了解`acvConfig`属性的用法。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

## 示例 2：元数据弹出窗口

使用各种属性来定义要使用信息图标查看的资源的元数据。信息弹出窗口提供有关资源或文件夹的信息集合，包括资源的标题、尺寸、修改日期、位置和描述。在下面的示例中，各种属性用于显示资源的元数据，例如，`repo:path` 属性指定资源的位置。<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

## 示例 3：边栏视图中的自定义过滤器属性

除了面向搜索之外，Assets Selector还允许您自定义各种属性，以细化从[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]应用程序进行的搜索。 添加以下代码以在应用程序中添加自定义搜索过滤器。 在下面的示例中，`Type Filter` 搜索过滤图像、文档或视频中的资源类型或已为搜索添加的过滤器类型。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->


>[!MORELIKETHIS]
>
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
>* [资产选择器上传](/help/assets/asset-selector-upload.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
