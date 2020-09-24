---
title: 为资产设置水印
description: 将水印添加到您的数字资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f1fcddf196a1a2bfa2629dbd6a8fe0ac057a3d07
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 为资产设置水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 允许您向图像添加数字水印。 [!DNL Assets] 支持将图像作为水印应用于其他图像文件。 水印可帮助用户验证资产的真实性和版权所有权。 此外，水印可用于指示文档的状态，如机密、草稿、有效性等。

要将Experience Manager配置为水印资产，请执行以下步骤：

1. PNG文件将作为水印应用。 将此文件上传到DAM存储库中。

1. 访问与您的环境关联的Cloud Manager Git存储库。 提交其Cloud Manager `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` Git存储库中名为的文件，其内容如下。 有关详细信息，请 [参阅如何将OSGi配置作为Experience Manager](/help/implementing/deploying/configuring-osgi.md)。

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [创建处理用户档案](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) ，以利用资产微服务应用水印。

   ![用于创建水印的资产处理用户档案](assets/watermark-processing-profile.png)

1. [将处理用户档案应用到文件夹](/help/assets/asset-microservices-configure-and-use.md#use-profiles) ，以创建带水印的资产。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用单个配置来为您的所有资产设置水印。 只有一幅图像用于水印，并且其宽度固定。
* 您可以将水印放置在中心，而无需拼贴。
* 不支持基于文本的水印。

>[!MORELIKETHIS]
>
>* [资产微服务概述](/help/assets/asset-microservices-overview.md)。
>* [将资产微服务与处理用户档案结合使用](/help/assets/asset-microservices-configure-and-use.md)。

