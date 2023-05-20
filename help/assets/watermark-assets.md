---
title: 為資產加上浮水印
description: 為您的數位資產新增浮水印。
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 12%

---

# 為您的資產加上浮水印 {#watermark-assets}

[!DNL Adobe Experience Manager Assets] 可讓您新增數位浮水印至影像。 [!DNL Assets] 支援將影像套用為其他影像檔案的浮水印。 浮水印可協助使用者驗證資產的真實性和版權所有權。 此外，浮水印可用於表示檔案的狀態，如機密性、草稿、有效性等。

進行設定 [!DNL Experience Manager] 若要為資產加上浮水印：

1. PNG檔案會套用為浮水印。 將此檔案上傳至您的DAM存放庫。

1. 導覽至 **[!UICONTROL 「工具>資產>資產設定」]**.

1. 按一下 **[!UICONTROL 系統浮水印設定檔]**.

1. 於 [!UICONTROL 系統浮水印設定檔頁面]，請指定在步驟1上傳至DAM存放庫的影像路徑。

1. 在中，指定相對於轉譯寬度的浮水印比例，範圍從0.0到1.0 **[!UICONTROL 縮放]** 欄位。

1. 单击“**[!UICONTROL 保存]**”。

   ![资源重复检测器](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >如果您已設定系統浮水印設定檔，使用 `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` 設定檔案（OSGi設定），您可以繼續使用，但Adobe建議使用新方法。


1. [建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) 以利用資產微服務來套用浮水印。

   ![用於建立浮水印的資產處理設定檔](assets/watermark-processing-profile.png)

   確保您啟用 **[!UICONTROL 浮水印]** 在建立處理設定檔時切換。

1. [將處理設定檔套用至資料夾](/help/assets/asset-microservices-configure-and-use.md#use-profiles) 以建立含水印的資產。

## 提示和限制 {#tips-limitations-bestpractices}

* 您可以使用單一設定來浮水印顯示所有資產。 只有一個影像用於浮水印，而且其寬度是固定的。
* 您可將浮水印放在中央而不需平鋪。
* 不支援文字型浮水印。

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

>[!MORELIKETHIS]
>
>* [資產微服務概覽](/help/assets/asset-microservices-overview.md).
>* [搭配處理設定檔使用資產微服務](/help/assets/asset-microservices-configure-and-use.md).

