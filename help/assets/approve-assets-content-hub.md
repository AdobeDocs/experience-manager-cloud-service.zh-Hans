---
title: 批准 Content Hub 的资产
description: 了解如何在Assetsas a Cloud Service中批准资源以使它们在Content Hub中可用。
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 6%

---

# 批准 Content Hub 的资产 {#approve-assets-content-hub}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![批准Content Hub的资源](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

品牌经理和营销人员对品牌资产进行严格控制。 只有获得批准的最新版本的资产才能在Content Hub中使用，从而确保所有渠道和应用程序之间的品牌一致性。

您可以使用AEM Assetsas a Cloud Service批准资源以简化资源管理，确保处理资源的过程受到控制且高效。

## 开始之前 {#pre-requisites}

在开始之前，您应该执行以下操作：

* 访问AEM Assetsas a Cloud Service

* 写入权限以编辑资源元数据，从而能够编辑资源的[资源属性](/help/assets/manage-organize-assets-view.md##manage-asset-status)中可用的&#x200B;**[!UICONTROL 状态]**&#x200B;字段。

## 批准 Content Hub 的资产{#approve-assets-for-content-hub}

Assetsas a Cloud Service中标记为`approved`的资源在Content Hub中自动可用。

>[!NOTE]
>
Assets as a Cloud Service和Content Hub必须使用相同的组织，才能在Content Hub中显示资产。

要使用AEM as a Cloud Service中的Assets视图将资源状态设置为`approved`，请执行以下操作：

1. 选择资源并单击工具栏中的&#x200B;**[!UICONTROL 详细信息]**。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 状态]**&#x200B;下拉列表中选择资源状态为`approved`。
1. 单击&#x200B;**[!UICONTROL 保存]**。

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

如果需要使用“管理员”视图批准资源，请参阅[使用管理员视图批准资源](/help/assets/approve-assets.md#approve-assets)。

## 使用Assets视图批量批准Content Hub的资源 {#bulk-approve-assets-content-hub}

使用适用于AEM Assetsas a Cloud Service的Assets视图批量批准资源。 批量批准的所有资源随后在Content Hub中可用。

要在Assets视图中批量批准文件夹内的资源，请执行以下操作：

1. 选择资源并单击&#x200B;**[!UICONTROL 批量元数据编辑]**。

1. 在右窗格的[!UICONTROL 属性]部分中的&#x200B;**[!UICONTROL 状态]**&#x200B;字段中选择&#x200B;**[!UICONTROL 已批准]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 在管理员视图中自动审批新摄取的资产 {#automate-approval-newly-ingested-assets}

从Assets视图切换到“管理员”视图后，您可以设置文件夹设置，以便添加到文件夹的所有新资源都能自动获得批准。

您可以通过以下方式在管理员视图和Assets视图之间切换：
![我的Workspace概述](assets/assets-view.png)

按照以下步骤在[!DNL Experience Manager Admin view]中自动审批新摄取的资产：

1. 在创作环境(https://author-pXXX-eYYY.adobeaemcloud.com)中创建文件夹。 将&#x200B;_XXX_&#x200B;替换为您的项目ID，将&#x200B;_YYY_&#x200B;替换为Experience Manager中的环境ID。
1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据配置文件]**。
1. 单击页面右上方的&#x200B;**[!UICONTROL 创建]**。
1. 添加配置文件标题并单击&#x200B;**[!UICONTROL 创建]**。 已成功创建元数据配置文件。
1. 选择新创建的元数据配置文件，然后单击&#x200B;**[!UICONTROL 编辑&#x200B;_(e)_]**。 <br>将打开&#x200B;**[!UICONTROL 编辑元数据配置文件]**表单，其中突出显示&#x200B;**[!UICONTROL 基本]**选项卡。
1. 将&#x200B;**[!UICONTROL 单行文本字段]**&#x200B;从右侧的&#x200B;**[!UICONTROL 构建表单]**&#x200B;分区拖放到表单中的元数据分区。
1. 单击新添加的字段，然后在&#x200B;**[!UICONTROL 设置]**&#x200B;面板中进行以下更新：
   1. 将&#x200B;**[!UICONTROL 字段标签]**&#x200B;更改为&#x200B;_已批准的Assets_。
   1. 将&#x200B;**[!UICONTROL 映射到属性]**&#x200B;的更新为&#x200B;_。/jcr：content/metadata/dam：status_。
   1. 将默认值更改为&#x200B;_已批准_。

1. 单击&#x200B;**[!UICONTROL 保存]**。
1. 在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择新创建的元数据配置文件。
1. 单击顶部操作栏中的&#x200B;**[!UICONTROL 将元数据配置文件应用到文件夹]**。
1. 选择要批准的文件夹，然后单击&#x200B;**[!UICONTROL 应用]**。
   <br>已将整个文件夹的权限设置为审批，并且任何上传到此文件夹的资产都会自动审批。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
此方法可批准文件夹中新创建的资产。 对于文件夹中的现有资源，您需要手动选择并批准它们。

## 管理使用Content Hub上传的资源 {#manage-assets-uploaded-using-content-hub}

[有权添加资源的Content Hub用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)可以[从本地文件系统向Content Hub添加资源](/help/assets/upload-brand-approved-assets.md)，或从OneDrive或Dropbox数据源导入资源。 所有资源都显示在Content Hub的顶层，这与本地文件系统或OneDrive和Dropbox数据源上可用的文件夹结构无关，以增强搜索功能。

是否显示使用Content Hub上传的资源，取决于您是否[启用了自动审批切换开关](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)：

* 如果启用了&#x200B;**[!UICONTROL 自动审批]**&#x200B;切换，则使用Content Hub上传的资源会自动可用。

* 如果禁用了&#x200B;**[!UICONTROL 自动审批]**&#x200B;切换功能，则使用Content Hub上传的资源不会自动显示。 这些资源位于Assetsas a Cloud Service环境的`hydrated-assets`文件夹中。 导航到文件夹，然后[批量编辑](#bulk-approve-assets-content-hub)这些资源的状态并更改为`Approved`，以便这些资源显示在Content Hub中。

![Content Hub审批流程](/help/assets/assets/content-hub-approval.png)
