---
title: 上传资产到存储库
description: 上传资产到 [!DNL Assets view]，查看上传状态，以及解决上传问题。
role: User
source-git-commit: c3076ce35128c147ce2056d11d9305d9a9456636
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 91%

---

# 上传资产 {#add-assets}

要添加新资产进行处理，请从本地文件系统上传几个资产。<!-- TBD: Many of the [common file formats are supported](/help/assets/supported-file-formats-assets-view.md). -->

您可以使用以下方法上传一个或多个资产或包含资产的文件夹：

* 将资产或文件夹拖动到用户界面上，然后按照屏幕上的说明操作。
* 在工具栏中单击&#x200B;**[!UICONTROL 添加资产]**&#x200B;选项并将一些文件添加到上传对话框。

<!-- TBD: Update this GIF
![Asset and nested folder upload demo](assets/do-not-localize/upload-assets.gif) -->

您可以使用任意这些方法在创建文件夹之后上传资产。要创建空文件夹，请在工具栏中单击&#x200B;**[!UICONTROL 创建文件夹]**。虽然 [!DNL Assets view] 提供了强大的全文搜索功能，您仍可以使用文件夹来更好地组织资产。

选择文件之后，您将看到确认对话框用于添加更多文件，或者删除已经选定的文件。要将更多文件添加到选择中，请单击&#x200B;**[!UICONTROL 浏览]**&#x200B;并选择&#x200B;**[!UICONTROL 浏览文件]**&#x200B;或&#x200B;**[!UICONTROL 浏览文件夹]**。从相同或不同文件夹添加多个文件或文件夹。

所有文件都列入队列后，单击&#x200B;**[!UICONTROL 上传]**。

![上传文件和文件夹](assets/upload-browse-files-folders.png)

*图：上传选定的资产后，您可以在队列中添加或删除资产。*

>[!TIP]
>
>如果将文件夹结构上传到“资产”视图，则无需使用该文件夹结构创建.ZIP文件，您可以直接上传文件夹结构。 上传到“资产”视图的.ZIP文件存储为一个ZIP资产，上传后不会自动提取。

## 查看上传进度和状态 {#upload-progress}

上传多个资产或嵌套文件夹到 [!DNL Assets view] 时，由于重复的资产或者网络问题等多种原因，一些资产可能会无法上传。

要跟踪上传进度，请单击工具栏中的&#x200B;**[!UICONTROL 上传进度]**&#x200B;选项。此时一个面板上显示所有资产的上传进度。

要根据上传的进度或状态查看资产的子集，请使用&#x200B;**[!UICONTROL 上传进度]**&#x200B;侧边栏中的筛选条件。不同的筛选条件可显示所有资产、已完成的上传、进行中的上传、排队等待上传的资产、已暂停的上传、重复的资产以及无法上传的资产。

![根据上传的状态筛选上传进度](assets/filter-upload-progress.png)

*图：根据资产的上传状态或上传进度，筛选您尝试上传的资产。*

资产上传之后，[!DNL Assets view] 立即处理资产以生成缩略图并处理元数据。对于较多的资产，处理需要一点时间。如果您未看到缩略图，但在占位符缩略图上看到正在处理消息，请在几分钟之后重新查看文件夹。处理期间，与其他内容一起，[!DNL Assets view] 生成演绎版、添加智能标记，并对资产详细信息编制索引以供搜索。

![资产在上传时处理，图块显示正在处理](assets/upload-processing.png)

*图：上传的资产在处理期间，在图块上显示正在处理。*

## 资产演绎版 {#renditions}

[!DNL Assets view] 近乎实时地处理上传的资产，并且对于许多支持的文件类型会生成演绎版。演绎版为图像创建，是上传图像的调整大小的版本。您不仅可以下载资产，还可以下载演绎版以使用合适的版本。在[预览某个资产](/help/assets/navigate-assets-view.md#preview-assets)时，您可以查看资产的所有演绎版。

![演绎版](assets/renditions-view-download.png)

*图：查看和下载演绎版*

## 管理失败的上传 {#resolve-upload-fails}

如果上传支持的资产由于某个原因失败，请在[!UICONTROL 上传进度]窗格中单击&#x200B;**[!UICONTROL 重试]**。

![重试失败的上传](assets/upload-retry.png)

*图：支持的文件由于某个原因上传失败时进行重试。*

如果您尝试上传重复的资产，则在您明确确认上传之前，这些资产不会上传。最初，重复的资产标记为失败的上传。要解决这个问题，您只需创建版本，也可以删除并替换现有资产或者通过重命名资产来创建重复副本。您可以逐个资产解决此类故障，也可以一次性批量解决所有失败的重复资产。

![逐个管理重复的资产](assets/uploads-manage-duplicates.png)

*图：对于默认情况下上传失败的重复资产，一次解决一个资产的问题。*

![批量管理所有失败的上传](assets/upload-progress-manage-failed-uploads.png)

*图：对于默认情况下上传失败的重复资产，一次性解决所有资产的问题。*

>[!TIP]
>
>您可以在中直接将资源上传到DAM存储库 [!DNL Creative Cloud] 桌面应用程序。
<!--TBD
See how [[!DNL Assets view] integrates with [!DNL Adobe Asset Link]](/help/assets/integration-assets-view.md).
-->

## 删除资产或文件夹 {#delete-assets}

用户可以删除不再需要的单独资产或文件夹。要删除某个资产或文件夹，请执行下列操作之一：

* 使用在资产或文件夹的缩略图上提供的选项。

  ![资产缩略图上显示的用于管理资产的选项](assets/options-on-thumbnail.png)

  *图：资产或文件夹图块上对文件和文件夹可用的操作。*

* 选择资产或文件夹，然后在工具栏中单击&#x200B;**[!UICONTROL 删除]** ![删除图标](assets/do-not-localize/delete-icon.png)。

## 后续步骤 {#next-steps}

* [观看视频，了解如何在“资源”视图中上传资源](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/creating.html)

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)
