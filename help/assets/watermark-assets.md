---
title: 对资产添加水印
description: 向数字资产添加水印。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 8%

---

# 对资产添加水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 用于向图像添加数字水印。 [!DNL Assets] 支持将图像作为水印应用到其他图像文件。 水印可帮助用户验证资产的真实性和版权所有权。 此外，水印可用于表示文档的状态，如机密、草稿、有效性等。

配置 [!DNL Experience Manager] 要对资产添加水印：

1. PNG文件将作为水印应用。 将此文件上传到DAM存储库。

1. 导航到 **[!UICONTROL 工具>资产>资产配置]**.

1. 单击 **[!UICONTROL 系统水印配置文件]**.

1. 在 [!UICONTROL “系统水印”配置文件页]，请在步骤1中指定上传到DAM存储库的图像路径。

1. 在 **[!UICONTROL 缩放]** 字段。

1. 单击“**[!UICONTROL 保存]**”。

   ![资源重复检测器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果您已使用 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 配置文件（OSGi配置），您可以继续使用它，但是，Adobe建议使用新方法。


1. [创建处理配置文件](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 利用资产微服务来应用水印。

   ![用于创建水印的资产处理配置文件](assets/watermark-processing-profile.png)

   确保启用 **[!UICONTROL 水印]** 在创建处理配置文件时进行切换。

1. [将处理配置文件应用到文件夹](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 创建带水印的资产。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用单个配置对所有资产添加水印。 只有一幅图像用于水印，其宽度是固定的。
* 您可以将水印放置在中心，而不进行拼贴。
* 不支持基于文本的水印。

**另请参阅**

* [翻译资产](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资产支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资产](use-assets-across-connected-assets-instances.md)
* [资源报表](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [资产微服务概述](/help/assets/asset-microservices-overview.md).
>* [将资产微服务与处理配置文件结合使用](/help/assets/asset-microservices-configure-and-use.md).

