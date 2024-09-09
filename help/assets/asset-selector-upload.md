---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资源选择器可在应用程序中搜索、查找和检索资源的元数据和演绎版。
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 将文件和文件夹上传到资源选择器 {#upload-files-folders}

您可以从本地文件系统将文件或文件夹上传到Asset Selector。 要使用本地文件系统上传文件，您通常需要使用Asset Selector微型前端应用程序提供的上传功能。

## 从本地文件系统上传资源 {#basic-upload}

要将资源添加到资源选择器，请执行以下步骤：

1. 如果您使用的是边栏视图，请转到省略号，然后单击![上传图标](assets/upload-icon.svg) **[!UICONTROL 上传]**。 另一方面，如果为模态视图，请单击右上角的![上载图标](assets/upload-icon.svg) **[!UICONTROL 上载]**。 出现[!UICONTROL 上传Assets]屏幕。

   ![将资源上传到资源选择器](assets/upload-assets.png)

   此外，在&#x200B;**[!UICONTROL 将文件或文件夹拖到此处]**&#x200B;部分中，您可以从本地文件系统拖动资源，或单击&#x200B;**[!UICONTROL 浏览]**&#x200B;以手动选择本地文件系统上可用的文件或文件夹。 作为上载的一部分，此文件列表以列表形式提供。

   ![将资产基本上传到资产选择器](assets/basic-upload.png)

   您还可以使用缩略图预览所选图像，然后单击X图标从列表中删除任何特定图像。 只有将鼠标悬停在图像名称或大小上时，才会显示X图标。 您还可以单击&#x200B;**[!UICONTROL 全部删除]**&#x200B;以从上载列表中删除所有项目。

1. 要完成上载过程，请单击&#x200B;**[!UICONTROL 上载]**。 此时会显示您上传的资产。 有关可配置代码，请参阅[基本上传](/help/assets/asset-selector-customization.md#basic-upload)。

## 上载包含元数据的资源 {#upload-assets-with-metadata}

您可以将元数据添加到资源，同时将资源立即上传到应用程序。 元数据包括各种字段，例如业务主题行、产品详细信息、促销活动等。 为此，使用了`metadataSchema`属性。 转到[资产选择器属性](/help/assets/asset-selector-properties.md)以了解有关`metadataSchema`属性的更多信息。

有关配置所需的代码段，请参阅[使用元数据](/help/assets/asset-selector-customization.md#upload-with-metadata)上传。

![上载包含元数据的资源](assets/upload-with-metadata.png)

1. 使用&#x200B;**[!UICONTROL 促销活动名称]**&#x200B;字段定义上载的名称。 您可以使用现有名称或创建新名称。 在键入名称时，资产选择器会为您提供更多选项。

   作为最佳实践，Adobe建议在其他字段中指定值，并且为上传的资源创建增强的搜索体验。

1. 同样，为&#x200B;**[!UICONTROL 关键字]**、**[!UICONTROL 渠道]**、**[!UICONTROL 时间范围]**&#x200B;和&#x200B;**[!UICONTROL 区域]**&#x200B;字段定义值。 通过按关键字、渠道和位置对资产进行标记和分组，使用您批准的公司内容的每个人都可以找到这些资产并保持其井然有序。

1. 单击&#x200B;**[!UICONTROL 上传]**&#x200B;以将资源上传到资源选择器。 [!UICONTROL 查看详细信息]确认框出现。 单击[!UICONTROL 继续]。

1. Assets开始上传。 单击[!UICONTROL 新建上载]以重新启动上载过程。 单击[!UICONTROL 完成]以完成上载。


## 自定义上载 {#customize-upload}

资产选择器允许您添加自定义上传表单。 提供了多种自定义设置。 例如，[hideUploadButton](/help/assets/asset-selector-properties.md)属性允许您隐藏应用程序中默认显示的上传按钮。 相反，您可以根据需要对其进行自定义，以在MFE应用程序之外呈现。 有关配置，请参阅[自定义上传](/help/assets/asset-selector-customization.md#customized-upload)。

![自定义上传](assets/customized-upload.png)

>[!MORELIKETHIS]
>
>* [资产选择器示例](/help/assets/asset-selector-examples.md)
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
