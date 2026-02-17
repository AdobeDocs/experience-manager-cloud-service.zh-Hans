---
title: 设置 Dynamic Media
description: 要设置Dynamic Media，必须配置Dynamic Media并管理图像和查看器预设。
mini-toc-levels: 3
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: bd43f86c9d3ad017a5e963800938e3ead98b7441
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 4%

---

# 设置 Dynamic Media {#setting-up-dynamic-media}

{{work-with-dynamic-media}}

[Dynamic Media](https://business.adobe.com/cn/products/experience-manager/assets/dynamic-media.html)通过按需提供丰富的可视化推销和营销资产帮助您管理资产，这些资产会自动扩展以用于Web、移动和社交网站上的使用。 通过使用一组主要源资产，Dynamic Media通过其可扩展、性能优化的全球网络实时生成和提供多种多样的丰富内容变体。

<!-- OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

如果您正在管理Dynamic Media，以下主题将是您感兴趣的主题：

* [配置 Dynamic Media](config-dm.md)
* [管理图像预设](managing-image-presets.md)
* [管理查看器预设](managing-viewer-presets.md)
* [Dynamic Media 疑难解答](troubleshoot-dm.md)

另请参阅以下主题：

* [视频编码和视频配置文件](video-profiles.md)
* [图像配置文件](image-profiles.md)

>[!NOTE]
>
>**如果您正在升级：**
>
>* Adobe [!DNL Experience Manager]启动并运行后，您上传的任何资源都会自动启用Dynamic Media（除非系统管理员明确禁用它）。 如果您在已升级的[!DNL Experience Manager]实例上并且是Dynamic Media的新用户，则可能必须重新处理您的资源以使其启用Dynamic Media。 请参阅[重新处理文件夹](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)中的资源。


## Dynamic Media证书续订需要一次性DNS更新 {#dns-update-dynamic-media-certificate-renewals}

如果您的域使用CAA（证书颁发机构授权）DNS记录，则必须授权DigiCert以允许继续续订Dynamic Media主机名使用的TLS/SSL证书。

在域的根(apex)添加以下CAA记录：

```
<yourdomain> CAA 0 issue "digicert.com"
```

这是一次性更改。

您可以使用DNS提供商工具或[CAA查找实用程序](https://caatest.co.uk/)来验证CAA记录是否存在。

如果存在CAA记录且DigiCert未获得授权，则当当前证书过期时，证书续订失败，这可能会导致图像和视频交付出现停机时间。 如果您的域不存在CAA记录，则无需执行任何操作。
