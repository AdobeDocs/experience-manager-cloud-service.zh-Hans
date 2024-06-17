---
title: 管理您的数字资源
description: 在  [!DNL Assets view] 中移动、删除、复制、重命名、更新您的资源和进行版本控制。
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 93%

---

# 管理资源 {#manage-assets}

您可以通过 [!DNL Assets view] 简单易用的用户界面，执行各种数字资源管理 (DAM) 任务。添加资源之后，您可以搜索、下载、移动、复制、重命名、删除、更新和编辑资源。

使用 [!DNL Assets view] 完成以下资源管理任务。选择某个资源时，顶部的工具栏显示以下选项。

![选中资源时的工具栏选项](assets/toolbar-image-selected.png)

*图：所选图像在工具栏中可用的选项。*

* ![“取消选择”图标](assets/do-not-localize/close-icon.png) 取消选择所选资源。

* ![“查找相似资源”图标](assets/do-not-localize/find-similar.svg) 根据元数据和智能标记在 Assets UI 中查找相似的图像资源。

* ![详细信息图标](assets/do-not-localize/edit-in-icon.png) 单击可预览资源并查看详细的元数据。在预览时，您可以查看版本并编辑图像。

* ![下载图标](assets/do-not-localize/download-icon.png) 将所选资源下载到您的本地文件系统。

* ![“添加到收藏集”图标](assets/do-not-localize/add-collection.svg) 将所选资源添加到收藏集。

* ![“固定资源”图标](assets/do-not-localize/pin-quick-access.svg) 固定资源，以供您在以后需要它时更快地访问它。所有固定的项目都显示在“我的工作区”的&#x200B;**快速访问**&#x200B;部分中。

* ![“在 Express 中编辑”图标](assets/do-not-localize/edit-e.svg) 在 Adobe Experience Manager Assets 中集成的 Adobe Express 中编辑图像。

* ![“编辑资源”图标](assets/do-not-localize/edit-e.svg) 使用 Adobe Express 编辑图像。

* ![“共享资源链接”图标](assets/do-not-localize/share-link.svg) 与其他用户共享某个资源的链接，以使其他用户可访问和下载该资源。

* ![“删除”图标](assets/do-not-localize/delete-icon.png) 删除所选的资源或文件夹。

* ![复制图标](assets/do-not-localize/copy-icon.png) 复制选定的文件或文件夹。

* ![移动图标](assets/do-not-localize/move-icon.png) 将选定的资源或文件夹移动到存储库层次结构中的不同位置。

* ![重命名图标](assets/do-not-localize/rename-icon.png) 重命名选定的资源或文件夹。请使用唯一名称，否则重命名将失败并出现警告。您可以使用新名称重试。
此外，您可以单击资产或文件夹的标题来重命名它。在 **重命名资产** 文本框中提及新文本，然后单击 **保存**。此功能可在网格、库、瀑布和列表视图中使用。

* ![瀑布视图图标](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布视图]。

* ![“复制到库”图标](assets/do-not-localize/copy-icon.png) 将资源添加到库。

* ![“分配任务”图标](assets/do-not-localize/review-delegate-icon.png) 将任务分配给其他用户以协作处理某个资源。

* ![“分配任务”图标](assets/do-not-localize/watch-asset.svg) 监控对资源执行的操作。

在资源缩略图上可以查看相同的选项。

![资源缩略图上显示的用于管理资源的选项](assets/options-on-thumbnail.png)

根据所选资源的类型，[!DNL Assets view] 在工具栏上仅显示相关的选项。

![选中资源时的工具栏选项](assets/toolbar-folder-selected.png)

*图：所选文件夹在工具栏中可用的选项。*

![选中资源时的工具栏选项](assets/toolbar-pdf-selected.png)

*图：所选 PDF 文件在工具栏中可用的选项。*

## 下载和分发资源 {#download}

您可以选择一个或多个资源或文件夹，或者两者的组合，然后将所选内容下载到本地文件系统。您可在 [!DNL Assets view] 之外编辑资源并重新上传或分发资源。您还可以[下载资源的演绎版](/help/assets/add-delete-assets-view.md#renditions)。

## 资源版本控制 {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

在对资源进行更新或编辑后重新上传资源时，[!DNL Assets view] 会对资源进行版本控制。您可以查看版本历史记录和过去的版本，并可将资源过去的某个版本恢复为最新版本，即在需要时还原到以前的版本。在以下场景中会创建资源版本：

* 在与现有资源相同的文件夹中，使用与现有资源相同的文件名上传新资源。[!DNL Assets view] 会提示您选择覆盖以前的资源，或者将新资源另存为一个版本。请参阅[上传重复的资源](/help/assets/add-delete-assets-view.md)。

  ![上传时创建版本](assets/uploads-manage-duplicates.png)

  *图：上传与现有资源具有相同名称的资源时，您可以创建资源的版本。*

* 编辑图像并单击&#x200B;**[!UICONTROL 另存为版本]**。请参阅[编辑图像](/help/assets/edit-images-assets-view.md)。

  ![将编辑后的图像另存为版本](assets/edit-image2.png)

  *图：将编辑后的图像另存为版本。*

* 打开现有资源的版本。单击&#x200B;**[!UICONTROL 新版本]**&#x200B;并将资源的更新版本上传到存储库中。

  ![版本历史记录中上传资源新版本的选项](assets/view-asset-versions2.png)

### 查看资源的版本 {#view-versions}

上传资源的重复副本或者修改后的副本时，您可以创建其版本。利用版本控制，您可以查看历史资源，并在需要时还原为以前的版本。

要查看版本，请打开资源的预览并单击右侧边栏中的&#x200B;**[!UICONTROL 版本]** ![版本图标](assets/do-not-localize/versions-clock-icon.png)。要预览特定版本，请选择该版本。要还原到该版本，请单击&#x200B;**[!UICONTROL 设为最新版本]**。

您还可以从版本时间线中创建版本。选择最新的版本，单击&#x200B;**[!UICONTROL 新版本]**，然后从本地文件系统上传资源的新副本。

![查看资源的版本](assets/view-asset-versions1.png)

*图：查看资源的版本，还原到以前的版本，或者上传另一个新版本。*

## 管理资源状态 {#manage-asset-status}

**所需的权限：资源的**`Can Edit`、`Owner` 或管理员权限。

通过“资源”视图，您可以为存储库中可用的资源设置状态。 设置资源状态以更好地治理和管理下游对数字资源的使用。

您可以为资源设置以下状态：

* 已批准

* 已拒绝

* 无状态

### 设置资源状态 {#set-asset-status}

要设置资源状态，请执行以下操作：

1. 选择资源并单击工具栏中的&#x200B;**[!UICONTROL 详细信息]**。

1. 在 **[!UICONTROL 基本]** 选项卡，从中选择资源状态 **[!UICONTROL 状态]** 下拉列表。 可能的值包括“已批准”、“已拒绝”和“无状态”（默认值）。

   >[!VIDEO](https://video.tv.adobe.com/v/342495)


### 设置资源过期日期 {#set-asset-expiration-date}

通过“资源”视图，您还可以设置存储库中可用资源的到期日期。 然后，可根据 `Expired` 资源状态[筛选搜索结果](search-assets-view.md#refine-search-results)。此外，还可指定资源的到期日期范围以进一步筛选搜索结果。

要设置资源过期日期，请执行以下操作：

1. 选择资源并单击工具栏中的&#x200B;**[!UICONTROL 详细信息]**。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，使用&#x200B;**[!UICONTROL 过期日期]**&#x200B;字段设置资源的过期日期。

`Expired`资源卡指示器会替代为资源设置的`Approved`或`Rejected`指示器。

您还可以根据资源状态筛选资源，有关更多信息，请参阅 [在“资源”视图中搜索资源](search-assets-view.md).

## 自定义元数据表单以包含资源状态字段 {#customize-asset-status-metadata-form}

**所需的权限：**&#x200B;管理员

默认情况下，资源视图提供了许多标准元数据字段。 组织有额外的元数据需求，就需要更多元数据字段以添加业务特有的元数据。企业可以利用元数据表单，将自定义元数据字段添加到资源的[!UICONTROL 详情]页面。特定于业务的元数据可以改进其资源的管理和发现。

有关如何将其他元数据字段添加到元数据表单的更多信息，请参阅[元数据表单](metadata-assets-view.md#metadata-forms)。

**将资源状态元数据字段添加到表单**

要将资源状态元数据字段添加到表单，请将&#x200B;**[!UICONTROL 资源状态]**&#x200B;组件从左边栏拖至表单中。将自动预填充映射属性。保存表单以确认更改。

**将过期日期元数据字段添加到表单**

要将过期日期元数据字段添加到表单，请将&#x200B;**[!UICONTROL 日期]**&#x200B;组件从左边栏拖至表单中。将&#x200B;**过期日期**&#x200B;指定为标签，并将`pur:expirationDate`指定为映射属性。保存表单以确认更改。

## 后续步骤 {#next-steps}

* [观看视频，了解如何在“资产”视图中进行资产管理](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/managing.html)

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)

