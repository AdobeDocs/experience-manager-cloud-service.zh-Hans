---
title: Publish到AEM和Dynamic Media的快速转换
description: Assets视图中的快速Publish允许您同时或单独将资源发布到AEM和Dynamic Media。 您可以选择资源和文件夹，然后选择发布到Dynamic Media或AEM。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 991888d532b3396054bd04c11c7257b61c337725
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 2%

---

# 发布资产到 AEM 和 Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

通过Experience Manager Assets，您可以使用Assets视图快速将资源发布到Experience Manager和Dynamic Media。 这可确保您管理资源，然后使用[Assets视图发布这些资源，而无需切换到“管理员”视图](/help/assets/overview.md##persona-based-experiences)。

Experience Manager Assets视图提供了灵活性，允许您将资源同时发布到AEM和/或Dynamic Media。 您可以在上传、浏览和搜索资产时发布资产。 本文详细介绍了用于发布资产的所有这些选项。

## 开始之前 {#before-you-begin}

配置这些设置以查看AEM和Dynamic Media的发布选项：

* 要查看Dynamic Media的发布选项，请使用“管理员”视图配置以下设置：

   * [创建Dynamic Media云配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
   * 在文件夹级别设置Dynamic Media Publish模式。 您也可以在创建Dynamic Media云配置时配置这些设置。 若要在文件夹级别覆盖这些设置，请参阅[在Dynamic Media中在文件夹级别配置选择性Publish](/help/assets/dynamic-media/selective-publishing.md)。

* 要查看AEM的发布选项，必须为环境配置AEM发布端点。

## 上传期间的Publish Assets {#piblish-assets-during-upload}

在将资源上传到文件夹时，您可以将资源发布到AEM和Dynamic Media。 显示的发布选项取决于上传资源的文件夹的Dynamic Media发布模式设置。 Dynamic Media发布模式可以设置为：

* **激活时：**&#x200B;将资源上传到此文件夹时，必须先明确发布资源，然后才能提供URL/嵌入链接。

* **立即：**&#x200B;将资源上传到此文件夹时，系统会将这些资源摄取到Experience Manager中，并立即提供URL/Embed。
* **选择性Publish：** Assets已发布到您选择的Experience Manager或Dynamic Media以在公共域中交付。

### Dynamic Media Publish模式设置为激活时 {#dynamic-media-publish-mode-set-to-upon-activation}

要在将资源上传到其Dynamic Media Publish模式设置为&#x200B;**激活时**&#x200B;的文件夹时发布资源，请执行以下操作：

1. 单击&#x200B;**添加Assets** > **浏览** > **浏览文件**&#x200B;以导航到相应的文件夹以上传资源。 **Publish选项**&#x200B;部分将&#x200B;**DM Publish模式**&#x200B;显示为&#x200B;**激活时**。
   ![激活时上传图像](/help/assets/assets/upload-uactivation.svg)
2. 选择&#x200B;**Publish到AEM和Dynamic Media**，然后单击&#x200B;**上传**。 资源将同时发布到AEM和Dynamic Media。 要查看这些资源的更新发布状态，请参阅[检查Publish状态](#check-publish-status)。

### Dynamic Media Publish模式设置为立即 {#dynamic-media-publish-mode-set-to-immediate}

要在将资源上传到Dynamic Media Publish模式设置为&#x200B;**立即**&#x200B;的文件夹时发布资源，请执行以下操作：

1. 单击&#x200B;**添加Assets** > **浏览** > **浏览文件**&#x200B;以导航到相应的文件夹以上传资源。 **Publish选项**&#x200B;部分将&#x200B;**DM Publish模式**&#x200B;显示为&#x200B;**立即**。
   ![文件上传图像 — 立即模式](/help/assets/assets/resized-image-pdf-svg-new.svg)


   由于Dynamic Media Publish模式为&#x200B;**立即**，因此当您单击&#x200B;**上传**&#x200B;时，上传的资源会自动发布到Dynamic Media。

2. 选择&#x200B;**Publish到AEM**&#x200B;以将上传的资源发布到AEM，然后单击“上传”。

   如果选择&#x200B;**Publish到AEM**，则资源将发布到AEM和Dynamic Media，否则资源将发布到Dynamic Media。

   要查看这些资源的更新发布状态，请参阅[检查Publish状态](#check-publish-status)。

### Dynamic Media Publish模式设置为选择性Publish {#dynamic-media-publish-mode-set-to-selective-publish}

要在将Dynamic Media Publish模式设置为&#x200B;**选择性Publish**&#x200B;的情况下将资源上传到文件夹，请执行以下操作：

1. 单击&#x200B;**添加Assets** > **浏览** > **浏览文件**&#x200B;以导航到相应的文件夹以上传资源。 **Publish选项**&#x200B;部分将&#x200B;**DM Publish模式**&#x200B;显示为&#x200B;**选择性Publish**。
   ![上载图像选择性管道模式](/help/assets/assets/upload-selective.svg)

2. 根据您的要求，选择&#x200B;**Publish到AEM**、**Publish到Dynamic Media**&#x200B;或两者，然后单击&#x200B;**上传**。

   资源会根据您的选择发布到AEM和Dynamic Media。

   要查看这些资源的更新发布状态，请参阅[检查Publish状态](#check-publish-status)。

## 使用asset browse页面的Publish资源 {#publish-assets-using-asset-browse-page}

要使用资源浏览页面发布资源，请执行以下操作：

1. 单击左窗格中可用的&#x200B;**Assets Management**&#x200B;部分中的&#x200B;**Assets**。
2. 选择需要发布的一个或多个资源或文件夹，然后单击&#x200B;**Publish**。
3. 选择&#x200B;**AEM**&#x200B;并单击&#x200B;**Publish**以将资源发布到AEM和Dynamic Media。
   ![资源浏览](/help/assets/assets/browse-uactivation-immediate.svg)
您无法发布Dynamic Media Publish模式设置为**选择性发布的文件夹。**所有其他选定的文件夹或资源在选择AEM后发布到AEM和Dynamic Media。
   ![资源浏览](/help/assets/assets/browse-selective123.svg)

## 使用搜索结果页面的Publish资源 {#publish-assets-using-search-results-page}

要使用资源搜索结果页面发布资源，请执行以下操作：

1. 在搜索栏中指定条件，然后单击搜索图标以查看结果。
2. 选择要发布的资源，然后单击&#x200B;**Publish。**
3. 根据您的要求选择AEM和/或Dynamic Media，然后单击&#x200B;**Publish。**
   ![搜索图像](/help/assets/assets/search-mode.svg)
在搜索结果页面上发布到Dynamic Media的选项取决于在存储库中可用资源的文件夹上设置的Dynamic Media Publish模式。

   >[!NOTE]
   >
   >如果您选择文件夹并单击搜索结果页面中的&#x200B;**Publish**，则Experience Manager Assets会显示一个将资产发布到AEM而不是Dynamic Media的选项，无论文件夹的Dynamic Media Publish模式设置如何。

## 检查Publish状态 {#check-publish-status}

要检查资产或文件夹的已发布状态，请执行以下操作：

1. 单击左窗格中可用的&#x200B;**[!UICONTROL Assets Management]**&#x200B;部分中的&#x200B;**[!UICONTROL Assets]**。
2. 使用视图切换器切换到列表视图。 您可以查看资源属性，如AEM发布、Dynamic Media Publish、标题、大小、维度等。\
   如果未发布资产或文件夹，列&#x200B;**AEM Publish**&#x200B;和&#x200B;**Dynamic Media Publish**&#x200B;的状态将显示为&#x200B;**不适用。**
   ![检查发布状态1](/help/assets/assets/check-publish-status1.png)
如果您无法在列表视图中查看AEM Publish和Dynamic Media Publish列：
   1. 单击![设置](/help/assets/assets/settings-icon.svg)并从&#x200B;**可配置的列**&#x200B;对话框中选择&#x200B;**AEM Publish**&#x200B;和&#x200B;**Dynamic Media Publish**&#x200B;列。
   2. 单击&#x200B;**确认。** Experience Manager Assets将选定的列添加到列表视图。

      ![检查发布状态2](/help/assets/assets/check-publish-status2.png)

您还可以通过选择资产并单击&#x200B;**详细信息来检查资产发布状态。**&#x200B;详细信息可在右侧窗格中的&#x200B;**Publish**&#x200B;部分中使用。 **Publish**&#x200B;部分列出了将资源发布到Dynamic Media和AEM的日期。 如果您需要查看资产的发布时间，可以导航到列表视图并查看这些详细信息。

![检查发布状态3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

将资产发布到AEM和Dynamic Media时，以下功能暂时不可用：

* 从Publish资源详细信息页面将其添加到AEM和Dynamic Media。
* 使用“快速Publish”向导可视化发布资源的端点。
* 在“快速Publish”向导中添加或删除更多资源。
* 查看已发布资源的页面。
* 能够在资源级别复制或粘贴Dynamic Media URL(如果已将资源发布到Dynamic Media)。
* 在发布到AEM时发布引用（资产、标记等）的功能。
* 能够在文件夹级别覆盖Dynamic Media同步状态。
* 能够在文件夹级别覆盖Dynamic Media Publish模式
* 尚不支持管理发布。
