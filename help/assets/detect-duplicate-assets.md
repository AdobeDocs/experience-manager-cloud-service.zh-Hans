---
title: 检测重复资产 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: 了解如何检测重复的资源
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: f18b8cf1922f05c0d7da2c58fb0a57bc5ff3d3b7
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 9%

---


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | 本文 |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=en) |

# 检测重复的资源 {#detect-duplicate-assets}

如果DAM用户上传一个或多个已存在于存储库中的资源， [!DNL Experience Manager] 检测复制并通知用户。 默认情况下禁用重复检测，因为它可能会产生性能影响，具体取决于存储库的大小和上传的资源数量。

要启用该功能，请执行以下操作：

1. 导航到 **[!UICONTROL 工具>资产>资产配置]**.

1. 单击 **[!UICONTROL 资源重复检测器]**.

1. 在 [!UICONTROL “资源重复检测器”页面]，单击 **[!UICONTROL 已启用]**.

   `dam:sha1` 检测元数据字段的值可确保即使文件名不同，也能检测到重复的资源。

1. 单击&#x200B;**[!UICONTROL 保存]**。

   ![资源重复检测器](assets/asset-duplication-detector.png)

>[!NOTE]
>
>如果您已使用配置重复检测器 `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` 配置文件（OSGi配置），您可以继续使用它，但Adobe建议使用新的方法。


启用后，Experience Manager会向Experience Manager收件箱发送重复资源的通知。 它是多个重复项的聚合结果。 用户可以选择根据结果删除资源。

![重复资产的收件箱通知](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>将资源上传到存储库时，Experience Manager会检测重复情况，并通知您前100个重复资源。
