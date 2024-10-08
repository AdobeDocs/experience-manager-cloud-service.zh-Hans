---
title: 在 [!DNL the Content Hub]中共享Assets
description: 在 [!DNL the Content Hub]中共享Assets
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 3%

---

# 在 Content Hub 共享资源 {#search-assets-as-a-link}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![共享资源横幅图像](assets/share-assets-banner.png)

通过链接共享资源是一种方便的方法，可使[!DNL the Content Hub]用户可以使用这些资源。 该功能允许授权用户访问和下载与其共享的资产。 从共享链接下载资源时，[!DNL the Content Hub]使用异步服务，该服务可提供更快且无中断的下载。

## 先决条件 {#prerequisites}

[Content Hub用户](deploy-content-hub.md#onboard-content-hub-users)可以执行本文中提到的操作。

## 共享单个资产 {#share-a-single-asset}

您可以通过执行以下步骤来共享单个资源：

1. 选择资产并单击![共享图标](assets/share.svg)图标可共享资产。

   ![共享单个资源](assets/sharing-single-asset.png)

1. 使用&#x200B;**[!UICONTROL 过期]**&#x200B;字段指定链接的过期日期。 选择一个可用选项，如24小时、1周、30天、90天、1年，或指定自定义日期。

1. 单击&#x200B;**[!UICONTROL 复制共享链接]**。 然后，您可以与收件人共享复制的链接。

## 共享多个资产 {#share-multiple-assets}

[!DNL The Content Hub]允许您通过共享链接共享多个资源。 执行以下步骤：

1. 选择需要与授权收件人共享的资源。 您可以逐个选择多个资源，或单击&#x200B;**[!UICONTROL 全选]**&#x200B;以一次选择所有可用资源。 仅当您至少选择一个资产时，才会显示&#x200B;**[!UICONTROL 全选]**&#x200B;选项。

1. 单击![共享图标](assets/share.svg)图标。

   ![共享多个资产](assets/sharing-multiple-assets.png)

1. 在预览部分中，您还可以根据要求删除资产。 使用&#x200B;**[!UICONTROL 过期]**&#x200B;字段指定链接的过期日期。 选择一个可用选项，如24小时、1周、30天、90天、1年，或指定自定义日期。

1. 单击&#x200B;**[!UICONTROL 复制共享链接]**。 然后，您可以与收件人共享复制的链接。

## 预览和共享资源 {#preview-assets}

您可以进行预览，以查看在与链接收件人共享之前，要共享的数字资产的外观。 单击需要预览的资源。 [!DNL Content Hub]显示资产](asset-properties-content-hub.md)的[详细视图。

单击![共享图标](assets/share.svg)图标可共享资产。 使用&#x200B;**[!UICONTROL 过期]**&#x200B;字段指定链接的过期日期。 选择一个可用选项，如24小时、1周、30天、90天、1年，或指定自定义日期。 单击&#x200B;**[!UICONTROL 复制共享链接]**。 然后，您可以与收件人共享复制的链接。

![在Content Hub中预览资源](assets/preview-assets-content-hub.png)

## 访问共享资源 {#access-shared-assets}

共享资产的链接后，授权的收件人可以单击该链接，在Web浏览器中预览或下载共享资产。

单击共享链接，然后单击资产卡上可用的下载图标以下载资产。  您还可以选择多个资产并单击&#x200B;**[!UICONTROL 下载]**。<!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub]将每个资源逐个下载到本地文件系统。

![访问共享链接](assets/content-hub-access-shared-links.png)
