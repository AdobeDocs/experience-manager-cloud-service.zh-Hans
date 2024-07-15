---
title: 图像的颜色标记
description: Adobe Experience Manager Assets使您能够区分图像中的颜色，并自动将这些颜色作为标记应用。 然后，您可以使用这些标记来搜索和过滤图像。
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
feature: Smart Imaging, Interactive Images, Asset Management
role: User, Admin
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# 图像的颜色标记 {#color-tag-images}

![颜色标记横幅](assets/banner-image.png)

Adobe Experience Manager (AEM) Assets使用Adobe Sensei AI功能区分图像中的颜色，并在摄取时自动将这些颜色作为标记应用。 这些标记可根据图像颜色组合来增强搜索体验。

您可以配置标记为图像的颜色数量（在1到40之间），以便以后可以根据这些颜色搜索图像。 Experience Manager Assets根据图像中的颜色覆盖范围来应用标记。 您还可以配置颜色标记的显示格式。

下图说明了在Experience Manager Assets中配置和管理图像的颜色标记时执行的一系列任务：

![颜色标记](assets/color-tagging-dfd.gif)

## 支持的文件格式 {#supported-file-formats-color-tags}

| 文件格式 | 扩展 | MIME类型 | 输入颜色空间 | 支持的最大源文件大小 | 支持的最大文件大小分辨率 |
|---|---|---|---|---|---|
| JPEG | .jpg和.jpeg | image/jpeg | sRGB | 15 GB | 20000 × 20000像素 |
| PNG | .png | image/png | sRGB | 15 GB | 20000 × 20000像素 |
| TIFF | .tif和.tiff | image/tiff | sRGB | 4 GB（受格式规范限制） | 20000 × 20000像素 |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB（受格式规范限制） | 20000 × 20000像素 |
| GIF | .gif | image/gif | sRGB | 15 GB | 20000 × 20000像素 |
| BMP | .bmp | image/bmp | sRGB | 4 GB（受格式规范限制） | 20000 × 20000像素 |

## 管理颜色标记属性 {#manage-color-tagging-properties}

要管理图像的颜色标记属性，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具> Assets >颜色标记]**。

   ![颜色标记属性](assets/color-tag-settings.png)

1. 在&#x200B;**[!UICONTROL 显示格式]**&#x200B;字段中指定颜色标记的显示格式。 可能的选项包括颜色名称、RGB或十六进制格式。

1. 在&#x200B;**[!UICONTROL 限制]**&#x200B;字段中指定要为图像标记的颜色数量。 当您查看图像的属性时，将显示这些颜色。 您可以在此字段中定义介于1和40之间的数字。 此字段的默认值为10色。

1. 在&#x200B;**[!UICONTROL 覆盖率/优势阈值%]**&#x200B;字段中指定最小颜色覆盖率百分比，以便在搜索结果中包含颜色标记。 例如，如果图像中红色颜色的覆盖率为10%，而您在此字段中定义了9%，则在搜索具有红色颜色的图像时，将会包含该图像。 但是，如果图像中红色颜色的覆盖率为10%，并且您在此字段中定义了11%，则在搜索具有红色颜色的图像时，不会包含该图像。

   您可以在此字段中指定介于5和100之间的任意数字。 默认值为 11。

   >[!NOTE]
   >
   >Adobe建议在此字段中使用接近默认值的值。 设置为此字段设置的高数值集（例如，大于25）可能会返回很少的搜索结果。 同样，设置低数值（例如，小于6）可能会返回太多的搜索结果，从而可能没有用。

1. 单击&#x200B;**[!UICONTROL 保存]**。


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### 禁用颜色标记 {#disable-color-tagging}

默认情况下，将启用图像的颜色标记。 您可以在文件夹级别禁用颜色标记。 所有子文件夹都从父文件夹继承颜色标记属性。

要在文件夹级别禁用颜色标记，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager > Assets >文件]**。

1. 选择文件夹并单击&#x200B;**[!UICONTROL 属性]**。

1. 在&#x200B;**[!UICONTROL 资产处理]**&#x200B;选项卡中，导航到&#x200B;**[!UICONTROL 图像的颜色标记]**&#x200B;文件夹。 从下拉列表中选择以下值之一：

   * 已继承 — 文件夹从父文件夹继承启用或禁用选项。

   * 启用 — 为选定的文件夹启用颜色标记。

   * 禁用 — 禁用所选文件夹的颜色标记。

   ![颜色标记设置](assets/color-tags-folder.png)

## 配置元数据架构以添加智能颜色标记组件 {#configure-metadata-schema}

元数据架构包含要填写的特定信息的特定字段。 它还包含布局信息，以便以用户友好的方式显示元数据字段。 元数据属性包括标题、描述、MIME类型、标记等。 您可以使用[!UICONTROL 元数据架构Forms]编辑器来修改现有架构或添加自定义元数据架构。

>[!NOTE]
>
>智能颜色标记字段在默认元数据架构中可用。 如果您使用的是自定义的元数据架构，请配置架构以添加智能颜色标记字段。

要将智能颜色标记组件添加到元数据架构表单编辑器，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具> Assets >元数据架构]**。

1. 选择架构名称并单击&#x200B;**[!UICONTROL 编辑]**。

1. 将&#x200B;**[!UICONTROL 智能颜色标记]**&#x200B;从&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡拖到&#x200B;**[!UICONTROL 元数据架构表单编辑器]**&#x200B;中。

1. 单击&#x200B;**[!UICONTROL 元数据架构表单编辑器]**&#x200B;中的&#x200B;**[!UICONTROL 智能颜色标记字段]**。

1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡的&#x200B;**[!UICONTROL 字段标签]**&#x200B;字段中指定适当的值。

1. 单击&#x200B;**[!UICONTROL 保存]**。

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## DAM中现有图像的颜色标记 {#color-tags-existing-images}

DAM中的现有图像不会自动进行颜色标记。 [!UICONTROL 手动重新处理Assets]以为其生成颜色标记。

要对资源存储库中存在的图像或资源文件夹（包括子文件夹）进行颜色标记，请执行以下步骤：

1. 选择[!DNL Adobe Experience Manager]徽标，然后从[!UICONTROL 导航]页面中选择资源。

1. 选择[!UICONTROL 文件]。

1. 在Assets界面中，导航到要应用颜色标记的文件夹。

1. 选择整个文件夹或特定图像。

1. 选择![重新处理资源图标](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新处理Assets]图标并选择[!UICONTROL 完整处理]选项。

进程完成后，导航到文件夹中任何图像的[!UICONTROL 属性]页面。 自动添加的标记显示在[!UICONTROL 基本]选项卡的[!UICONTROL 智能颜色标记]部分中。


## 查看图像的智能颜色标记 {#view-color-tags}

要查看图像的智能颜色标记，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager > Assets >文件]**。

1. 单击相应的文件夹，然后选择图像。

1. 选择&#x200B;**[!UICONTROL 属性]**&#x200B;并查看&#x200B;**[!UICONTROL 智能颜色标记]**&#x200B;字段中的标记。

   ![查看颜色标记](assets/view-color-tags.png)

   将鼠标悬停在颜色标记上，以便可以查看图像中颜色的&#x200B;**[!UICONTROL 覆盖率/优势阈值%]**。

## 配置AEM Assets颜色谓词 {#configure-search-predicate}

您可以为图像配置搜索过滤器。 然后，您可以根据特定颜色来筛选结果。

>[!NOTE]
>
>仅当您未使用默认搜索表单时，才配置AEM Assets颜色谓词。

要配置搜索过滤器，请使用Assets管理员搜索边栏创建资源颜色谓词。

要配置搜索过滤器，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具>常规>搜索Forms]**。

1. 选择&#x200B;**[!UICONTROL Assets管理员搜索边栏]**，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 将&#x200B;**[!UICONTROL 资源颜色谓词]**&#x200B;从&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡拖到&#x200B;**[!UICONTROL 搜索表单编辑器]**。

1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡的&#x200B;**[!UICONTROL 字段标签]**&#x200B;字段中指定适当的值。

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存设置。

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## 根据颜色搜索图像 {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

在配置所有颜色标记属性和[配置Assets颜色谓词](#search-images-based-on-colors)后，您可以基于颜色作为过滤器来搜索图像。

要根据颜色搜索图像，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Assets >文件]**。

1. 从下拉列表中选择&#x200B;**[!UICONTROL 筛选器]**。
   ![筛选Assets](assets/filter-assets.png)

1. 选择[AEM Assets颜色谓词](#configure-search-predicate)。

1. 拖动拾色器以选择相应的颜色。 所选的颜色将显示在拾色器下方的只读字段中。 可以选择RGB或十六进制作为颜色的显示格式。

   ![拾色器](assets/color-picker-color-tags.png)

   您可以根据选择的一种颜色来过滤图像。 将选定颜色作为智能颜色标记之一并超过[覆盖率/优势阈值%](#manage-color-tagging-settings)的图像将显示在右侧窗格中。

1. 单击搜索栏中的X可清除过滤器。

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
