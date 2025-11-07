---
title: 快速发布到 [!DNL AEM and Dynamic Media]
description: 通过 [!DNL Assets view] 中的快速发布，可同时或单独将资产发布到 [!DNL AEM and Dynamic Media] 。 您可以选择资源和文件夹，然后选择发布到 [!DNL Dynamic Media] 或 [!DNL AEM]。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing
role: User
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# 将Assets发布到[!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

通过[!DNL Experience Manager Assets]，您可以使用[!DNL Experience Manager]快速将资源发布到[!DNL Dynamic Media]和[!DNL Assets view]。 这可确保您管理资产，然后使用[[!DNL Assets view] 发布资产，而无需切换到 [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences)。

[!DNL Experience Manager Assets view]提供了灵活性，可以将资源同时发布到[!DNL AEM]和[!DNL Dynamic Media]，或同时发布到两者。 您可以在上传、浏览和搜索资产时发布资产。 本文详细介绍了用于发布资产的所有这些选项。

## 开始之前 {#before-you-begin}

配置这些设置以查看[!DNL AEM and Dynamic Media]的发布选项：

* 要查看[!DNL Dynamic Media]的发布选项，请使用“管理员”视图配置以下设置：

   * [创建 [!DNL Dynamic Media] 云配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。
   * 在文件夹级别设置[!DNL Dynamic Media]发布模式。 您也可以在创建[!DNL Dynamic Media]云配置时配置这些设置。 要在文件夹级别覆盖这些设置，请参阅[在 [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md)中配置文件夹级别的选择性发布。

* 要查看[!DNL AEM]的发布选项，必须为环境配置[!DNL AEM]发布终结点。

## 在上传期间发布Assets {#piblish-assets-during-upload}

在将资源上传到文件夹时，您可以将资源发布到[!DNL AEM and Dynamic Media]。 显示的发布选项取决于将上传资产的文件夹的[!DNL Dynamic Media]发布模式设置。 [!DNL Dynamic Media]发布模式可以设置为：

* **[!UICONTROL 激活时]：**&#x200B;将资源上传到此文件夹时，必须先明确发布资源，然后才能提供URL/嵌入链接。

* **[!UICONTROL 立即]：**&#x200B;将资源上传到此文件夹时，系统会将这些资源摄取到Experience Manager并立即提供URL/Embed。
* **[!UICONTROL 选择性发布]：** Assets已发布到您选择的[!DNL Experience Manager]或[!DNL Dynamic Media]以在公共域中交付。

### 激活时[!UICONTROL Dynamic Media发布模式]设置为 {#dynamic-media-publish-mode-set-to-upon-activation}

要在将资产上传到其[!DNL Dynamic Media Publish Mode]设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;的文件夹时发布资产，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL 添加Assets]** > **[!UICONTROL 浏览]** > **[!UICONTROL 浏览文件]**&#x200B;以导航到相应的文件夹以上传资源。 **[!UICONTROL 发布选项]**&#x200B;部分在激活时&#x200B;**[!UICONTROL 将]** DM发布模式&#x200B;**[!UICONTROL 显示为]**。

   ![激活时上传图像](/help/assets/assets/upload-uactivation.svg)

1. 选择&#x200B;**[!UICONTROL 发布到AEM和Dynamic Media]**，然后单击&#x200B;**[!UICONTROL 上传]**。 资产将同时发布到[!DNL AEM and Dynamic Media]。 要查看这些资源的更新发布状态，请参阅[检查发布状态](#check-publish-status)。

### [!UICONTROL Dynamic Media发布模式]设置为[!UICONTROL 立即] {#dynamic-media-publish-mode-set-to-immediate}

要在将资源上传到其[!UICONTROL Dynamic Media发布模式]设置为&#x200B;**[!UICONTROL 立即]**&#x200B;的文件夹时发布资源，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL 添加Assets]** > **[!UICONTROL 浏览]** > **[!UICONTROL 浏览文件]**&#x200B;以导航到相应的文件夹以上传资源。 **[!UICONTROL 发布选项]**&#x200B;部分将&#x200B;**[!UICONTROL DM发布模式]**&#x200B;显示为&#x200B;**[!UICONTROL 立即]**。

   ![文件上传图像 — 立即模式](/help/assets/assets/resized-image-pdf-svg-new.svg)

   由于[!UICONTROL Dynamic Media发布模式]为&#x200B;**[!UICONTROL 立即]**，因此当您单击[!DNL Dynamic Media]上传&#x200B;**[!UICONTROL 时，上传的资源会自动发布到]**。

1. 选择&#x200B;**发布到AEM**&#x200B;以将上传的资源发布到[!DNL AEM]，然后单击&#x200B;**[!UICONTROL 上传]**。

   如果您选择&#x200B;**发布到AEM**，则资源将发布到[!DNL AEM and Dynamic Media]，否则资源将发布到[!DNL Dynamic Media]。

   要查看这些资源的更新发布状态，请参阅[检查发布状态](#check-publish-status)。

### [!UICONTROL Dynamic Media发布模式]设置为[!UICONTROL 选择性发布] {#dynamic-media-publish-mode-set-to-selective-publish}

要在将[!UICONTROL Dynamic Media发布模式]设置为&#x200B;**[!UICONTROL 选择性发布]**&#x200B;的文件夹上载期间发布资产，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL 添加Assets]** > **[!UICONTROL 浏览]** > **[!UICONTROL 浏览文件]**&#x200B;以导航到相应的文件夹以上传资源。 **[!UICONTROL 发布选项]**&#x200B;部分将&#x200B;**[!UICONTROL DM发布模式]**&#x200B;显示为&#x200B;**[!UICONTROL 选择性发布]**。

![上载图像选择性管道模式](/help/assets/assets/upload-selective.svg)

1. 根据您的要求，选择&#x200B;**[!UICONTROL 发布到AEM]**、**[!UICONTROL 发布到Dynamic Media]**&#x200B;或同时选择两者，然后单击&#x200B;**上传**。

   资源已根据您的选择发布到[!DNL AEM and Dynamic Media]。

   要查看这些资源的更新发布状态，请参阅[检查发布状态](#check-publish-status)。

## 使用资源浏览页面发布资源 {#publish-assets-using-asset-browse-page}

要使用资源浏览页面发布资源，请执行以下操作：

1. 单击左窗格中可用的&#x200B;**[!UICONTROL Assets Management]**&#x200B;部分中的&#x200B;**[!UICONTROL Assets]**。
1. 选择您需要发布的一个或多个资源或文件夹，然后单击&#x200B;**[!UICONTROL 发布]**。
1. 选择&#x200B;**[!UICONTROL AEM]**&#x200B;并单击&#x200B;**[!UICONTROL 发布]**&#x200B;以将资源发布到[!DNL AEM and Dynamic Media]。

   ![资源浏览](/help/assets/assets/browse-uactivation-immediate.svg)

   您无法发布[!DNL Dynamic Media]发布模式设置为&#x200B;**[!UICONTROL 选择性发布]**&#x200B;的文件夹。 所有其他选定的文件夹或资产在选择[!DNL AEM and Dynamic Media]后发布到[!DNL AEM]。

   ![资源浏览](/help/assets/assets/browse-selective123.svg)

## 使用搜索结果页面发布资源 {#publish-assets-using-search-results-page}

要使用资源搜索结果页面发布资源，请执行以下操作：

1. 在搜索栏中指定条件，然后单击搜索图标以查看结果。
1. 选择需要发布的资源并单击&#x200B;**[!UICONTROL 发布]。**
1. 根据您的要求选择[!DNL AEM, Dynamic Media]或两者，然后单击&#x200B;**[!UICONTROL 发布]**。

   ![搜索图像](/help/assets/assets/search-mode.svg)

   在搜索结果页面上发布到[!DNL Dynamic Media]的选项取决于在存储库中可用资产的文件夹上设置的[!DNL Dynamic Media]发布模式。

   >[!NOTE]
   >
   >如果选择文件夹并单击搜索结果页面中的&#x200B;**[!UICONTROL 发布]**，则[!DNL Experience Manager Assets]将显示一个选项，可将资产发布到[!DNL AEM]而不是[!DNL Dynamic Media]，而不管文件夹的[!DNL Dynamic Media]发布模式设置如何。

## 检查发布状态 {#check-publish-status}

要检查资产或文件夹的已发布状态，请执行以下操作：

1. 单击左窗格中可用的&#x200B;**[!UICONTROL Assets Management]**&#x200B;部分中的&#x200B;**[!UICONTROL Assets]**。
1. 使用视图切换器切换到列表视图。 您可以查看资源属性，如[!UICONTROL AEM发布]、[!UICONTROL Dynamic Media发布]、[!UICONTROL 标题]、[!UICONTROL 大小]、[!UICONTROL 维度]等。

   如果未发布资源或文件夹，列&#x200B;**[!UICONTROL AEM Publish]**&#x200B;和&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;的状态将显示为&#x200B;**[!UICONTROL N/A]**。

   ![检查发布状态 1](/help/assets/assets/check-publish-status1.png)

   如果您无法在列表视图中查看[!DNL AEM]发布和[!DNL Dynamic Media]发布列：

   1. 单击![设置](/help/assets/assets/settings-icon.svg)并从&#x200B;**[!UICONTROL 可配置的列]**&#x200B;对话框中选择&#x200B;**[!UICONTROL AEM发布]**&#x200B;和&#x200B;**[!UICONTROL Dynamic Media发布]**&#x200B;列。
   1. 单击&#x200B;**[!UICONTROL 确认]**。 [!DNL Experience Manager Assets]将选定的列添加到列表视图。

      ![检查发布状态2](/help/assets/assets/check-publish-status2.png)

您还可以通过选择资产并单击&#x200B;**[!UICONTROL 详细信息]**&#x200B;来检查资产发布状态。 详细信息可在右侧窗格中的&#x200B;**[!UICONTROL 发布]**&#x200B;部分中使用。 **[!UICONTROL 发布]**&#x200B;部分列出了将资源发布到[!DNL Dynamic Media]和[!DNL AEM]的日期。 如果您需要查看资产的发布时间，可以导航到列表视图并查看这些详细信息。

![检查发布状态3](/help/assets/assets/check-publish-status3.png)

## 限制 {#limitations}

将资产发布到[!DNL AEM and Dynamic Media]时，以下功能暂时超出范围：

* 从[!DNL AEM and Dynamic Media]将资源发布到[!DNL Asset details page]。
* 使用快速发布向导可视化发布资产的端点。
* 在“快速发布”向导中添加或删除更多资源。
* 查看已发布资源的页面。
* 能够在资源级别复制或粘贴[!DNL Dynamic Media] URL（如果资源已发布到[!DNL Dynamic Media]）。
* 能够在发布到[!DNL AEM]时发布引用（资产、标记等）。
* 能够在文件夹级别覆盖[!DNL Dynamic Media]同步状态。
* 能够在文件夹级别覆盖[!DNL Dynamic Media]发布模式
* 尚不支持管理发布。
