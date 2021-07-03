---
title: 对资产添加水印
description: 向数字资产添加水印。
contentOwner: AG
feature: 资产管理，发布
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 对资产添加水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 用于向图像添加数字水印。[!DNL Assets] 支持将图像作为水印应用到其他图像文件。水印可帮助用户验证资产的真实性和版权所有权。 此外，水印可用于表示文档的状态，如机密、草稿、有效性等。

要配置[!DNL Experience Manager]以对资产添加水印，请执行以下步骤：

1. PNG文件将作为水印应用。 在DAM存储库中上传此文件。

1. 访问与您的环境关联的[!DNL Cloud Manager] Git存储库。 在存储库中提交名为`com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json`的文件，其中包含以下内容。 有关说明，请参阅 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)中的[如何进行OSGi配置。

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [创建处理配](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 置文件以利用资产微服务来应用水印。

   ![用于创建水印的资产处理配置文件](assets/watermark-processing-profile.png)

1. [将处理配置文件应用到文件夹](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 以创建带水印的资产。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用单个配置对所有资产添加水印。 只有一幅图像用于水印，其宽度是固定的。
* 您可以将水印放置在中心，而不进行拼贴。
* 不支持基于文本的水印。

>[!MORELIKETHIS]
>
>* [资产微服务概述](/help/assets/asset-microservices-overview.md)。
>* [将资产微服务与处理配置文件结合使用](/help/assets/asset-microservices-configure-and-use.md)。

