---
title: 全景图像
description: 瞭解如何在Dynamic Media中使用全景影像。
contentOwner: Rick Brough
feature: Panoramic Images
role: User
exl-id: bdc5d00e-fa92-4db5-a3b2-4dd5885eec0b
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 2%

---

# 全景影像{#panoramic-images}

本節說明如何使用「全景影像」檢視器來轉譯球面全景影像，以獲得房間、屬性、位置或橫向的360度沈浸式檢視體驗。

另請參閱 [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以與全景影像檢視器搭配使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

若要讓上傳的資產符合您要與全景影像檢視器一起使用的球面全景影像資格，資產必須具備下列其中一項或兩項條件：

* 外觀比例為2。

<!--  You can override the default aspect ratio setting of 2 in CRXDE Lite at the following:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content` -->
* 以關鍵字標籤 `equirectangular`，或 `spherical`和 `panorama`，或 `spherical` 和 `panoramic`. 另請參閱 [使用標籤](/help/sites-cloud/authoring/features/tags.md).

外觀比例和關鍵字條件都適用於資產詳細資訊頁面和 `Panoramic Media` wcm元件。

若要上傳資產以與全景影像檢視器搭配使用，請參閱 [上傳資產](/help/assets/manage-digital-assets.md#uploading-assets).

<!--  NEED TO CHECK IF DM CLASSIC PART OF SKYLINE 

## Configuring Dynamic Media Classic (Scene7) {#configuring-dynamic-media-classic-scene}

For the Panoramic Image viewer to work properly within AEM, you must synchronize the Panoramic Image viewer presets with Dynamic Media Classic (Scene7) and Dynamic Media Classic (Scene7)-specific metadata so the viewer presets get updated in the JCR. To accomplish this, configure Dynamic Media Classic (Scene7) in the following manner:

1. Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account.

1. Near the upper-right corner of the page, navigate to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
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

1. At the bottom of the Image Server Publish page, on the left side, select **[!UICONTROL Save]**.

1. In the lower-right corner, select **[!UICONTROL Close]**.

### Troubleshooting the Panoramic Media WCM component {#troubleshooting-the-panoramic-media-wcm-component}

If you dropped an image into the Panoramic Media component in your WCM and the component placeholder collapsed, you may want to troubleshoot the following:

* If you experience a 403 Forbidden error, it may have been caused by the requested image size being too large. Review the **[!UICONTROL Reply Image Size Limit]** settings in [Configuring Dynamic Media Classic (Scene7)](/help/assets/dynamic-media/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

* For an "Invalid lock" on the asset or "Parsing error" displayed on the page, check Request Obfuscation Mode and Request Locking Mode to ensure they are disabled.
* For a tainted canvas error, setup a Rule Set Definition File Path and Invalidate CTN for the previous requests for the image asset.
* If image quality becomes very low after an image request with sizing above the supported limit, check that the **[!UICONTROL JPEG Encoding Attributes > Quality]** setting is not empty. A typical setting for the **[!UICONTROL Quality]** field is `95`. You can find the setting on the Image Server Publish page. To access the page, see [Configuring Dynamic Media Classic (Scene7)](/help/assets/dynamic-media/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

-->

## 預覽全景影像 {#previewing-panoramic-images}

另請參閱 [預覽資產](/help/assets/dynamic-media/previewing-assets.md).

## 發佈全景影像 {#publishing-panoramic-images}

另請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
