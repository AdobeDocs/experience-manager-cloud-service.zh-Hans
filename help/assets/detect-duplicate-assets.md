---
title: 检测 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]的重复资源
description: 了解如何检测重复的资源
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 9%

---


# 检测重复的资产 {#detect-duplicate-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

如果DAM用户上传一个或多个已存在于存储库中的资源，[!DNL Experience Manager]将检测重复并通知用户。 默认情况下禁用重复检测，因为它可能会产生性能影响，具体取决于存储库的大小和上传的资源数量。

要启用该功能，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具> Assets > Assets配置]**。

1. 单击&#x200B;**[!UICONTROL 资源重复检测器]**。

1. 在[!UICONTROL 资产重复检测器页面]上，单击&#x200B;**[!UICONTROL 已启用]**。

   “检测元数据”字段的`dam:sha1`值可确保即使文件名不同，也能检测到重复的资源。

1. 单击&#x200B;**[!UICONTROL 保存]**。

   ![资源重复检测器](assets/asset-duplication-detector.png)

>[!NOTE]
>
>如果您已使用`/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json`配置文件（OSGi配置）配置了重复检测器，则可以继续使用它，但是Adobe建议使用新方法。


启用后，Experience Manager会将重复资源的通知发送到Experience Manager收件箱。 它是多个重复项的聚合结果。 用户可以选择根据结果删除资源。

![重复的资产的收件箱通知](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>将资源上传到存储库时，Experience Manager会检测重复情况，并通知您前100个重复资源。
