---
title: 签入和签出 [!DNL Assets]中的文件
description: 了解如何签出资源以进行编辑，并在更改完成后重新签入。
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 10%

---

# 在[!DNL Experience Manager] DAM中签入和签出文件 {#check-in-and-check-out-files-in-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Experience Manager Assets]允许您签出要编辑的资产，并在完成更改后重新签入。 签出资源后，只有您可以编辑、注释、发布、移动或删除资源。 签出资产会锁定资产。 在将资源签回到[!DNL Assets]之前，其他用户无法对资源执行任何此类操作。 但是，他们仍可以更改锁定的资源的元数据。

要能够签出/签入资产，您需要具有资产的“写入”权限。

此功能有助于防止其他用户覆盖作者所做的更改，即多个用户跨团队协作编辑工作流。

## 签出资产 {#checking-out-assets}

1. 从[!DNL Assets]用户界面中，选择要签出的资产。 您还可以选择要签出的多个资源。

1. 在工具栏中，单击&#x200B;**[!UICONTROL 签出]**。 **[!UICONTROL 签出]**&#x200B;选项切换到&#x200B;**[!UICONTROL 签入]**。
要验证其他用户是否可以编辑您签出的资产，请以其他用户的身份登录。 图标![签出锁定图标](assets/do-not-localize/checkout_lock.png)显示在您签出的资源的缩略图上。

   卡片视图中的![签出图标](assets/checkout-icon-card-view.png)

   选择资源。 请注意，工具栏不显示任何允许您编辑、批注、发布或删除资源的选项。

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   要编辑锁定的资源的元数据，请单击&#x200B;**[!UICONTROL 查看属性]**。

1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以在编辑模式下打开资产。

1. 编辑资源并保存更改。 例如，裁切图像并保存。 您还可以选择对资源添加注释或发布。

1. 从[!DNL Assets]界面中选择已编辑的资源，然后单击工具栏中的&#x200B;**[!UICONTROL 签入]**。 已修改的资产已签入[!DNL Assets]，可供其他用户编辑。

## 强制签入 {#forced-check-in}

管理员可以签入其他用户签出的资源。

1. 以管理员身份登录到[!DNL Assets]。
1. 从[!DNL Assets]用户界面中选择一个或多个已由其他用户签出的资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 释放锁定]**。 资产将重新签入，并且可供其他用户编辑。

## 最佳实践和限制 {#tips-limitations}

* 可能会删除包含已签出资源文件的&#x200B;*文件夹*。 在删除文件夹之前，请确保用户未签出任何数字资产。

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

>[!MORELIKETHIS]
>
>* [了解签入和签出 [!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解签入和签出的视频教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)
