---
title: 将品牌批准的资产上传到 [!DNL Content Hub]
description: 了解如何将品牌批准的资产上传到Content Hub
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# 将品牌批准的资产上传到Content Hub {#upload-brand-approved-assets-content-hub}

管理员可以将资源从本地文件系统添加到Content Hub，或从OneDrive或Dropbox数据源导入资源。 所有资源都显示在Content Hub的顶层，这与本地文件系统或OneDrive和Dropbox数据源上可用的文件夹结构无关，以增强搜索功能。

为了进一步增强资产搜索，Content Hub允许您：

* 定义与资源上传相关的关键详细信息，如促销活动名称、关键字、渠道等。

* 成功上传后为每个资源自动生成更多属性，例如文件大小、格式、分辨率和其他某些属性。

* 使用由提供的人工智能 [Adobe Sensei](https://www.adobe.com/cn/sensei.html) 以自动将相关标记应用于您上传的所有资源。 这些标记名为智能标记，有助于您快速查找相关资产，从而提高项目的内容速度。

确保仅上传 [将批准的资源品牌化到Content Hub](/help/assets/approve-assets.md).

![上传品牌批准的资产](assets/upload-brand-approved-assets.png)

## 先决条件 {#prerequisites-add-assets}

[有权添加资源的Content Hub用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) 可以将资源上传到Content Hub。

## 将资源从本地文件系统添加到Content Hub {#add-assets-local-file-system}

要将资源添加到Content Hub，请执行以下步骤：

1. 单击 **[!UICONTROL 添加Assets]** 查看 **[!UICONTROL 添加已批准的资产]** 对话框创建上载。

1. 在 **[!UICONTROL 将文件或文件夹拖到此处]** 部分中，您可以从本地文件系统拖动资源或单击 **[!UICONTROL 浏览]** 手动选择本地文件系统中可用的文件或文件夹。 作为上载的一部分，此文件列表以列表形式提供。


   您还可以使用缩略图预览所选图像，然后单击X图标从列表中删除任何特定图像。 只有将鼠标悬停在图像名称或大小上时，才会显示X图标。 您还可以单击 **[!UICONTROL 全部移除]** 以从上载列表中删除所有项目。

   完成上传过程并启用 **[!UICONTROL “上载”按钮]**，您必须使用Campaign名称对资产进行分组。

   ![将资源上传到Content Hub](assets/upload-assets-content-hub.png)

1. 使用定义上载的名称 **[!UICONTROL 营销活动名称]** 字段。 您可以使用现有名称或创建新名称。 键入名称时，Content Hub会为您提供更多选项。 <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   作为最佳实践，Adobe建议在其他字段中指定值，并且为上传的资源创建增强的搜索体验。

1. 同样，定义 **[!UICONTROL 关键字]**， **[!UICONTROL 渠道]**， **[!UICONTROL 时间范围]**、和 **[!UICONTROL 区域]** 字段。 通过按关键字、渠道和位置对资产进行标记和分组，使用您批准的公司内容的每个人都可以找到这些资产并保持其井然有序。

1. 单击 **[!UICONTROL 上传]** 以将资源上传到Content Hub。 [!UICONTROL 查看详细信息] 出现确认框。 单击[!UICONTROL 继续]。

1. Assets开始上传。 单击 [!UICONTROL 新建上传] 以重新启动上载过程。 单击 [!UICONTROL 完成] 以完成上载。

管理员还可以配置上传资产时显示的必填和可选字段，例如营销策划名称、关键字、渠道等。 有关更多信息，请参阅 [配置Content Hub用户界面](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## 将资源从OneDrive或Dropbox数据源添加到Content Hub {#add-assets-onedrive-dropbox}

要将资源从OneDrive或Dropbox数据源添加到Content Hub，请执行以下操作：

1. 单击 **[!UICONTROL 添加Assets]** 查看 **[!UICONTROL 添加已批准的资产]** 用于从OneDrive或Dropbox导入资源的对话框。

1. 单击 **[!UICONTROL OneDrive]** 或 **[!UICONTROL Dropbox]** 以启动导入流程。 Content Hub会提示您登录OneDrive或Dropbox帐户，然后在左窗格中显示您的OneDrive或Dropbox文件夹结构。

1. 单击文件旁边的+图标或文件夹名称，以查看选定项目列表中的项目。 选择需要添加到Content Hub门户的所有文件后，重复步骤3至6 [将资源从本地文件系统添加到Content Hub](#add-assets-local-file-system) 以完成上传过程。

   ![从OneDrive或Dropbox将资源上传到Content Hub](assets/add-assets-onedrive-dropbox.png)

管理员还可以配置上传资产时显示的必填和可选字段，例如营销策划名称、关键字、渠道等。 有关更多信息，请参阅 [配置Content Hub用户界面](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

