---
title: 下载资源
description: 從下載資產 [!DNL Adobe Experience Manager Assets] 和啟用或停用下載功能。
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 5%

---

# 從下載資產 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service | 本文 |

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接透過傳送包含資產連結的電子郵件 [!DNL Adobe Experience Manager Assets]. 下載的資產會整合在ZIP檔案中。 <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

無法下載下列資產型別：影像集、迴轉集、混合媒體集和轉盤集。

您可以使用下列方法，從Experience Manager下載資產：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager使用者介面](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 下載資產，使用 [!DNL Experience Manager] 介面 {#download-assets}

Experience Manager會根據資產數量和大小最佳化下載體驗。 從使用者介面即時下載較小檔案。 [!DNL Experience Manager] 直接下載原始檔案的單一資產請求，而不是將單一資產封存在ZIP封存中，以便更快進行下載。 Experience Manager支援使用非同步請求進行大型下載。 大於100 GB的下載請求會分割為多個ZIP封存檔，每個封存檔的大小上限為100 GB。

依預設， [!DNL Experience Manager] 在中觸發通知 [[!DNL Experience Manager] 收件匣](/help/sites-cloud/authoring/getting-started/inbox.md) 產生下載封存時。

![收件匣通知](assets/inbox-notification-for-large-downloads.png)


### 為大型下載啟用電子郵件通知 {#enable-emails-for-large-downloads}

在下列任一情況下，都會觸發非同步下載：

* 如果有十個以上的資產
* 如果下載大小超過100 MB
* 如果下載的準備時間超過30秒

當非同步下載在後端執行時，使用者可以繼續探索並進一步在Experience Manager中工作。 除了Experience Manager收件匣通知外，Experience Manager還可以傳送電子郵件以在下載程式完成時通知使用者。 若要啟用此功能，管理員可透過以下方式設定電子郵件服務 [設定SMTP伺服器連線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

設定電子郵件服務後，管理員和使用者可以從Experience Manager介面啟用電子郵件通知。

若要啟用電子郵件通知：

1. 登入 [!DNL Experience Manager Assets].
1. 從右上角按一下使用者圖示，然後按一下 **[!UICONTROL 我的偏好設定]** 以開啟「使用者偏好設定」視窗。
1. 選取 **[!UICONTROL 資產下載電子郵件通知]** 核取方塊並按一下 **[!UICONTROL Accept]**.

   ![enable-email-notifications-for-large-download](/help/assets/assets/enable-email-for-large-downloads.png)


若要下載資產，請遵循下列步驟：

1. 在 [!DNL Experience Manager] 使用者介面，按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要下載的資產。 選取資料夾或選取資料夾內的一或多個資產。 在工具列上，按一下 **[!UICONTROL 下載]**.

   ![從下載資產時可用的選項 [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. 在下載對話方塊中，選取您想要的下載選項。

   | 下載選項 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资产创建单独的文件夹]** | 選取此選項，為每個資產建立一個資料夾，其中包含資產的所有已下載轉譯。 如果取消選取，每個資產（以及如果選取下載其轉譯）都會包含在所產生封存檔的父資料夾中。 |
   | **[!UICONTROL 电子邮件]** | 選取此選項可將電子郵件通知（包含下載連結）傳送給其他使用者。 收件者使用者必須是 `dam-users` 群組。 標準電子郵件範本可在下列位置取得：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您部署期間自訂的範本可在下列位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以將租使用者特定的自訂範本儲存在下列位置：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资产]** | 選取此選項，即可以原始格式下載資產。<br>如果原始資產有子資產，則可以使用子資產選項。 |
   | **[!UICONTROL 演绎版]** | 轉譯是資產的二進位表示法。 資產具有主要代表性 — 上傳檔案的主要代表性。 它們可以有任意數量的表示。 <br> 使用此選項，您可以選取要下載的轉譯。 可用的轉譯取決於您選取的資產。 |
   | **[!UICONTROL 智能裁剪]** | 選取此選項，即可從下載內所選資產的所有智慧型裁切轉譯 [!DNL Experience Manager]. 已建立包含「智慧型裁切」轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 动态演绎版]** | 選取此選項可即時產生一系列替代轉譯。 選取此選項時，您也可以從以下專案選取，以選取要動態建立的轉譯： [影像預設集](/help/assets/dynamic-media/image-presets.md) 清單。 <br>此外，您也可以選取大小與測量單位、格式、色域、解析度，以及任何選用的影像修飾元（例如反轉影像）。 只有當您有以下條件時，才可使用選項： [!DNL Dynamic Media] 已啟用。 |

1. 在對話方塊中，按一下 **[!UICONTROL 下載]**.

   如果大型下載已啟用電子郵件通知，則收件匣中會顯示包含封存zip資料夾之下載URL的電子郵件。 按一下電子郵件中的下載連結以下載zip封存。

   ![適用於大型下載的電子郵件通知](/help/assets/assets/email-for-large-notification.png)

   您也可以在以下位置檢視通知： [!DNL Experience Manager] 收件匣。

   ![inbox-notifications-for-large-download](/help/assets/assets/inbox-notification-for-large-downloads.png)

## 下載使用連結共用所共用的資產 {#link-share-download}

使用連結共用資產是可讓感興趣的人使用的便利方式，無需他們登入 [!DNL Assets]. 另請參閱 [連結共用功能](/help/assets/share-assets.md#sharelink).

使用者從共用連結下載資產時， [!DNL Assets] 使用非同步服務，提供更快速且無中斷的下載。 要下載的資產會在背景的收件匣中排入佇列，放入可管理檔案大小的ZIP封存檔中。 對於較大的下載專案，下載會區塊化為100 GB的檔案。

此 [!UICONTROL 下載收件匣] 顯示每個封存的處理狀態。 處理完成後，您可以從收件匣下載封存。

![下載收件匣](assets/link-sharing-download-inbox.png)

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設servlet [!DNL Experience Manager] 可讓已驗證身分的使用者發出任意大型的並行下載請求，以建立資產的ZIP檔案。 下載準備可能會影響效能，甚至可能使伺服器和網路過載。 若要降低此功能所導致的類似DoS的潛在風險， `AssetDownloadServlet` 發佈執行個體已停用OSGi元件。 如果您不需要作者執行個體的下載功能，請停用作者的servlet。

若要允許從您的DAM下載資產，例如在使用Asset Share Commons或其他類似入口網站的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議將允許的下載大小設定為儘可能的低，而不影響日常下載需求。 高值可能會影響效能。

1. 以定位發佈執行模式的命名慣例建立資料夾，即 `config.publish`：

   `/apps/<your-app-name>/config.publish`

1. 在設定資料夾中，建立型別為的新檔案 `nt:file` 已命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 填入 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` ，如下所示。 將下載的大小上限（以位元組為單位）設定為 `asset.download.prezip.maxcontentsize`. 以下範例將ZIP下載的大小上限設定為不超過100 KB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

如果您不需要下載功能，請停用servlet以防止任何類似DoS的風險。 此 `Asset Download Servlet` 可以在上停用 [!DNL Experience Manager] 更新Dispatcher設定以封鎖任何資產下載請求，從而製作和發佈執行個體。 也可以直接透過OSGi主控台手動停用servlet。

1. 若要透過Dispatcher設定封鎖資產下載請求，編輯 `dispatcher.any` 設定並將新規則新增至 [篩選區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## 提示和限制 {#tips-limitations}

* 如果您下載空白資料夾， [!DNL Experience Manager] 傳達有關建立ZIP封存的成功訊息，但封存並未建立。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [下載受DRM保護的資產](drm.md)
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [使用支援的Adobe Creative Cloud應用程式中的Adobe資產連結下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

