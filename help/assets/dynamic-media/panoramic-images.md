---
title: 全景图像
description: 了解如何在Dynamic Media中处理全景图像。
feature: 全景图像
role: User
exl-id: bdc5d00e-fa92-4db5-a3b2-4dd5885eec0b
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 5%

---

# 全景图像{#panoramic-images}

本节介绍如何使用全景图像查看器来渲染球形全景图像，以便在室内、属性、位置或横向享受沉浸式360°的观看体验。

另请参阅[管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

![全景图像2](assets/panoramic-image2.png)

## 上传资产以与全景图像查看器一起使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

要将上传的资产限定为要与全景图像查看器一起使用的球形全景图像，该资产必须具有以下任一项或两项：

* 宽高比为2。

<!--  You can override the default aspect ratio setting of 2 in CRXDE Lite at the following:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content` -->
* 使用关键字`equirectangular`、`spherical`和`panorama`或`spherical`和`panoramic`进行标记。 请参阅[使用标记](/help/sites-cloud/authoring/features/tags.md)。

纵横比和关键字条件都适用于资产详细信息页面和`Panoramic Media` WCM组件的全景资产。

要上传资产以与全景图像查看器一起使用，请参阅[上传资产](/help/assets/manage-digital-assets.md#uploading-assets)。

<!--  NEED TO CHECK IF DM CLASSIC PART OF SKYLINE 

## Configuring Dynamic Media Classic (Scene7) {#configuring-dynamic-media-classic-scene}

For the Panoramic Image viewer to work properly within AEM, you must synchronize the Panoramic Image viewer presets with Dynamic Media Classic (Scene7) and Dynamic Media Classic (Scene7)-specific metadata so the viewer presets get updated in the JCR. To accomplish this, configure Dynamic Media Classic (Scene7) in the following manner:

1. Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account.

1. Near the upper-right corner of the page, click **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.
1. On the Image Server Publish page, from the **[!UICONTROL Publish Context]** drop-down menu near the top, select **[!UICONTROL Image Serving]**.

1. On the same Image Server Publish page, locate the heading **[!UICONTROL Request Attributes]**.
1. Under the Request Attributes heading, locate **[!UICONTROL Reply Image Size Limit]**. Then, in the associated Width and Height fields, increase the maximum allowable image size for panoramic images.

   Dynamic Media Classic (Scene7) has a limit of 25,000,000 pixels. The maximum allowable size for images with a 2:1 aspect ratio is 7000 x 3500. However, for typical desktop screens, 4096 x 2048 pixels is sufficient.

   >[!NOTE]
   >
   >Only images that fall within the maximum allowable image size are supported. Requests for images that are above the size limit will result in a 403 response.

1. Under the Request Attributes heading, do the following:

    * Set Request Obfuscation Mode to **[!UICONTROL Disabled]**.
    * Set Request Locking Mode to **[!UICONTROL Disabled]**.

   These settings are necessary for using the `Panoramic Media` WCM component in AEM.

1. At the bottom of the Image Server Publish page, on the left side, click **[!UICONTROL Save]**.

1. In the lower-right corner, click **[!UICONTROL Close]**.

### Troubleshooting the Panoramic Media WCM component {#troubleshooting-the-panoramic-media-wcm-component}

If you dropped an image into the Panoramic Media component in your WCM and the component placeholder collapsed, you may want to troubleshoot the following:

* If you experience a 403 Forbidden error, it may have been caused by the requested image size being too large. Review the **[!UICONTROL Reply Image Size Limit]** settings in [Configuring Dynamic Media Classic (Scene7)](/help/assets/dynamic-media/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

* For an "Invalid lock" on the asset or "Parsing error" displayed on the page, check Request Obfuscation Mode and Request Locking Mode to ensure they are disabled.
* For a tainted canvas error, setup a Rule Set Definition File Path and Invalidate CTN for the previous requests for the image asset.
* If image quality becomes very low after an image request with sizing above the supported limit, check that the **[!UICONTROL JPEG Encoding Attributes > Quality]** setting is not empty. A typical setting for the **[!UICONTROL Quality]** field is `95`. You can find the setting on the Image Server Publish page. To access the page, see [Configuring Dynamic Media Classic (Scene7)](/help/assets/dynamic-media/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

-->

## 预览全景图像 {#previewing-panoramic-images}

请参阅[预览资产](/help/assets/dynamic-media/previewing-assets.md)。

## 发布全景图像 {#publishing-panoramic-images}

请参阅[发布资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。
