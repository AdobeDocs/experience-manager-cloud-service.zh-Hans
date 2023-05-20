---
title: 資產分析
description: 追蹤協力廠商網站、行銷活動和Adobe創意解決方案中所使用影像的使用者評分和使用情況統計資料。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 11%

---

# 資產分析 {#asset-insights}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | 本文 |

Assets Insights功能可讓您追蹤用於協力廠商網站、行銷活動和Adobe創意解決方案之影像的使用者評分和使用情況統計資料。 它有助於提供影像效能和人氣的相關深入分析。

Assets Insights會擷取使用者活動詳細資訊，例如影像的評分、點按和曝光次數（影像載入網站上的次數）。 系統會根據這些統計資料，將分數指派給影像。 您可以使用分數和效能統計資料來選取要包含在目錄、行銷活動等中的熱門影像。 您甚至可以根據這些統計資料制定封存和授權更新政策。

若要讓Assets Insights從網站擷取影像的使用狀況統計資料，您必須在網站程式碼中包含影像的內嵌程式碼。

若要讓Assets Insights顯示資產的使用狀況統計資料，請先設定功能以從中擷取報表資料 [!DNL Adobe Analytics]. 如需詳細資訊，請參閱 [設定資產分析](#configure-asset-insights). 若要使用此功能，請購買 [!DNL Adobe Analytics] 另外授權。

>[!NOTE]
>
>僅支援並提供影像的深入分析。

## 檢視影像的統計資料 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視Assets Insights分數。

1. 從「資產」使用者介面中，選取影像，然後按一下 **[!UICONTROL 屬性]** （從工具列）。
1. 在「屬性」頁面中，按一下 **[!UICONTROL 深入分析]**.
1. 在中檢閱資產的使用方式詳細資訊 **[!UICONTROL 深入分析]** 標籤。 此 **[!UICONTROL 分數]** 區段說明資產的資產使用總量和效能損失。

   使用分數說明資產在各種解決方案中的使用次數。

   此 **[!UICONTROL 曝光次數]** score是資產在網站上載入的次數。 以下顯示的數字： **[!UICONTROL 點按次數]** 是資產的點按次數。

1. 檢閱 **[!UICONTROL 使用狀況統計資料]** 區段，以瞭解資產所屬的實體，以及最近使用過資產的創意解決方案。 使用量越高，該資產在使用者中受歡迎的可能性就越大。 使用情況資料會顯示在下列標題下：

   * **[!UICONTROL 資產]**：資產成為集合或複合資產一部分的次數。
   * **[!UICONTROL 網頁與行動]**：資產屬於網站和應用程式的次數。
   * **[!UICONTROL 社交]**：資產在其他解決方案中的使用次數，例如 [!DNL Adobe Campaign].
   * **[!UICONTROL 電子郵件]**：資產在電子郵件行銷活動中的使用次數。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >因為Assets Insights功能通常會從擷取解決方案資料 [!DNL Adobe Analytics] 解決方案區段可能不會定期顯示最新資料。 資料顯示的時間長度取決於Assets Insights為擷取Analytics資料而執行的擷取作業排程。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」段落中的資料不同，「效能統計資料」段落會顯示最新的資料。

1. 若要取得您包含在網站中資產的內嵌程式碼，以取得效能資料，請按一下 **[!UICONTROL 取得內嵌程式碼]** 在資產縮圖下方。 <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 檢視影像的彙總統計資料 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在「資產」使用者介面中，導覽至包含您要檢視其見解的資產的資料夾。
1. 按一下 **[!UICONTROL 版面]** 選項，然後選擇 **[!UICONTROL 深入分析檢視]**.
1. 頁面會顯示資產的使用情況分數。 比較各種資產的評等並得出深入見解。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 設定資產分析 {#configure-asset-insights}

[!DNL Experience Manager Assets] 從擷取有關協力廠商網站使用的數位資產的使用資料 [!DNL Adobe Analytics]. 若要啟用Assets Insights以擷取此資料並產生深入分析，請先設定要與整合的功能 [!DNL Adobe Analytics].

>[!NOTE]
>
>僅支援並為影像提供深入分析。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。

1. 如需Analytics Web服務存取資訊，請前往 **[!UICONTROL 分析]** > **[!UICONTROL 管理員]** > **[!UICONTROL 管理工具]** > **[!UICONTROL 公司設定]** > **[!UICONTROL 網站服務]** 並複製 **[!UICONTROL 共用機密]** 金鑰。

   在精靈中，選取 **[!UICONTROL 資料中心]**，並提供 **[!UICONTROL 公司]**、網站服務 **[!UICONTROL 使用者名稱]**，並貼上 **[!UICONTROL 共用機密]** 金鑰。

   按一下 **[!UICONTROL 驗證]**.

   ![設定Adobe Analytics以在中分析資產 [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *圖：設定Adobe Analytics以在中分析資產[!DNL Experience Manager]*

1. 在成功驗證後，您將會在下拉式清單中取得報表套裝。 選取Adobe Analytics **[!UICONTROL 報表套裝]** 從您希望Assets Insights擷取資料的位置。 按一下 **[!UICONTROL 新增]**.

1. 晚於 [!DNL Experience Manager] 設定您的報表套裝，按一下 **[!UICONTROL 完成]**.

如需詳細資訊，請參閱 [Adobe Analytics網站服務](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### 頁面追蹤器 {#page-tracker}

在您設定Adobe Analytics帳戶後，系統就會為您產生頁面追蹤器程式碼。 啟用Assets Insights以追蹤 [!DNL Experience Manager] 用於第三方網站的資產，請在網站程式碼中包含頁面追蹤器程式碼。 使用Assets中的頁面追蹤器公用程式，產生頁面追蹤器程式碼。 <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 按一下 **[!UICONTROL 下載]** 以下載頁面追蹤器程式碼。

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
下列範常式式碼片段會顯示範例網頁中包含的頁面追蹤器程式碼：

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

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
