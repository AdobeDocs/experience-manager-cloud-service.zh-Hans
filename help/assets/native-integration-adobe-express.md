---
title: AEM Assets与Adobe Express的本机集成
description: AEM Assets与Adobe Express本机集成允许您从Adobe Express用户界面中直接访问AEM Assets中存储的资源。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 9044d5cefe7064a015c18c988e29b8c2e8088bae
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 21%

---

# 与Adobe Express的本机集成 {#native-integration-adobe-express}

AEM Assets 与 Adobe Express 在本地集成，允许您直接从 Adobe Express 用户界面访问存储在 AEM Assets 中的资源。可将在 AEM Assets 中管理的内容放入 Express 画布，然后将新内容或经过编辑的内容保存在 AEM Assets 存储库中。该集成具有以下主要优势：

* 通过在AEM中编辑和保存新资源提高了内容重复使用率。

* 减少了创建新资产或创建新版本现有资产的总体时间和工作量。

## 先决条件 {#prerequisites}

有权访问AEM Assets中的Adobe Express和至少一个环境。 该环境可以是 Assets as a Cloud Service 或 Assets Essentials 中的任何存储库。


## 在 Adobe Express 编辑器中使用 AEM Assets {#use-aem-assets-in-express}

执行以下步骤以开始在Adobe Express编辑器中使用AEM Assets：

1. 打开 Adobe Express Web 应用程序。

2. 通过加载新模板或项目或创建资源来打开新的空白画布。

3. 单击 **[!UICONTROL 资产]** 在左侧导航窗格中可用。 Adobe Express显示您有权访问的存储库列表，以及在根级别可用的资源和文件夹列表。

4. 浏览或搜索存储库中的资产以拖放到画布上。 您可以使用各种可用的过滤器来筛选资源，例如文件类型、MIME类型和维度。

   >[!NOTE]
   >
   >按维度过滤不适用于视频。

   ![从 Assets 加载项纳入资源](assets/adobe-express-native-integration.png)


## 将 Adobe Express 项目保存在 AEM Assets 中 {#save-express-projects-in-assets}

在 Express 画布中纳入适当的修改后，即可将该画布保存在 AEM Assets 存储库中。

1. 单击 **[!UICONTROL 共享]** 以打开 **[!UICONTROL 共享]** 对话框。

   ![将资源保存在 AEM 中](assets/adobe-express-share.png)

2. 从右窗格的“Storage（存储）”部分中选择， **AEM Assets**. Adobe Express显示“上载”对话框。
3. 指定资源的名称和格式。您可以以PNG、JPEG、PDF、MP4、MP4+PNG或MP4+JPEG格式保存画布内容。 格式会根据资源自动进行调整。

   >[!NOTE]
   >
   >选择“当前页面”会将文件保存到目标文件夹中。 选择“所有页面”会在目标中为所有非PDF文件创建一个新文件夹，并将它们保存在该位置，而PDF文件会作为单个文件保存到目标文件夹中。

4. 单击下的文本区域 **目标文件夹** 以选择位置并保存资产。

   ![将资源保存在 AEM 中](/help/assets/assets/page-selection-and-destination-folder.png)

5. 可选：您可以使用为上传添加营销活动元数据 **项目或营销活动名称** 字段。 您可以使用现有名称或创建新名称。 您可以为上传定义多个项目或营销策划名称。 要注册名称，只需键入名称并按Enter键即可。
作为最佳实践，Adobe建议在其他字段中指定值，并且为上传的资源创建增强的搜索体验。

6. 同样，定义 **[!UICONTROL 关键字]** 和 **[!UICONTROL 渠道]** 字段。

7. 单击 **[!UICONTROL 上传]** 以将资源上传到AEM Assets。




## 限制 {#limitations}

1. 对于导入和导出，支持的视频文件类型为MP4。

2. 对于MP4视频导入：

   a)支持的最大文件大小为200 MB。 如果超过此限制，将显示一条警告消息。
b)支持的最大分辨率是3840 X 3840像素。
c)不支持具有透明背景（Alpha通道）的视频。

3. 对于MP4视频导出：

   a)支持的最大文件大小为200 MB。 如果超过此限制，将显示一条警告消息，其中包含下图中显示的解决方法建议
   ![带有解决方法的警报](/help/assets/assets/alert-with-workaround.png).
