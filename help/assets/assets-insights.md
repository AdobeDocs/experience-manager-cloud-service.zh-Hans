---
title: Assets Insights
description: 跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用统计数据。
contentOwner: AG
feature: Asset Insights, Asset Reports
role: User, Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 12%

---

# Assets Insights {#asset-insights}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | 本文 |

通过Assets Insights功能，您可以跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。 它有助于提供有关图像的性能和常用程度的洞察。

Assets Insights会捕获用户活动详细信息，例如对图像进行评级、单击的次数和展示次数（图像加载到网站上的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和性能统计信息选择热门图像以将其包含在目录、营销活动等中。 您甚至可以根据这些统计数据制定存档和许可证更新策略。

要让Assets Insights从网站中捕获图像的使用情况统计数据，您必须在网站代码中包含该图像的嵌入代码。

要让Assets Insights显示资源的使用情况统计数据，请首先配置该功能以从[!DNL Adobe Analytics]获取报表数据。 有关详细信息，请参阅[配置Assets分析](#configure-asset-insights)。 若要使用此功能，请单独购买[!DNL Adobe Analytics]许可证。

>[!NOTE]
>
>仅支持并提供图像分析。

## 查看图像的统计信息 {#viewing-statistics-for-an-image}

您可以从元数据页面查看Assets Insights分数。

1. 从Assets用户界面中，选择图像，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。
1. 在“属性”页面中，单击&#x200B;**[!UICONTROL 分析]**。
1. 在&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡中查看资产的使用情况详细信息。 **[!UICONTROL 得分]**&#x200B;部分描述了资源的总使用情况和性能损失。

   使用情况得分描述了资产在各种解决方案中的使用次数。

   **[!UICONTROL 展示次数]**&#x200B;分数是资源加载到网站上的次数。 在&#x200B;**[!UICONTROL 点击次数]**&#x200B;下显示的数量是点击资产的次数。

1. 查看&#x200B;**[!UICONTROL 使用情况统计数据]**&#x200B;部分，了解资产所属的实体以及最近使用它的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **[!UICONTROL 资源]**：资源属于收藏集或复合资源的次数。
   * **[!UICONTROL Web和移动设备]**：资产成为网站和应用程序一部分的次数。
   * **[!UICONTROL Social]**：在其他解决方案（如[!DNL Adobe Campaign]）中使用资产的次数。
   * **[!UICONTROL 电子邮件]**：在电子邮件营销活动中使用该资源的次数。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于Assets Insights功能通常会定期从[!DNL Adobe Analytics]中获取解决方案数据，因此“解决方案”部分可能不会显示最新数据。 显示数据的时间段取决于Assets Insights为检索Analytics数据而运行的获取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计信息”部分显示最新数据。

1. 若要获取您在网站中包含的资产嵌入代码以获取性能数据，请单击资产缩略图下方的&#x200B;**[!UICONTROL 获取嵌入代码]**。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 查看图像的聚合统计信息 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在Assets用户界面中，导航到包含要查看其分析的资源的文件夹。
1. 单击工具栏中的&#x200B;**[!UICONTROL 布局]**&#x200B;选项，然后选择&#x200B;**[!UICONTROL 分析视图]**。
1. 页面显示资源的使用分数。 比较各种资源的评级并得出见解。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 配置Assets分析 {#configure-asset-insights}

[!DNL Experience Manager Assets]从[!DNL Adobe Analytics]中获取有关第三方网站使用的数字资产的使用情况数据。 要启用Assets Insights以检索此数据并生成见解，请首先配置该功能以与[!DNL Adobe Analytics]集成。

>[!NOTE]
>
>仅支持图像并提供见解。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。

1. 有关Analytics Web服务访问信息，请转到&#x200B;**[!UICONTROL Analytics]** > **[!UICONTROL 管理员]** > **[!UICONTROL 管理工具]** > **[!UICONTROL 公司设置]** > **[!UICONTROL Web服务]**，并复制&#x200B;**[!UICONTROL 共享密钥]**&#x200B;密钥。

   在向导中，选择&#x200B;**[!UICONTROL 数据中心]**，提供&#x200B;**[!UICONTROL 公司]**、Web服务&#x200B;**[!UICONTROL 用户名]**&#x200B;的显示名称，并粘贴&#x200B;**[!UICONTROL 共享密钥]**。

   单击&#x200B;**[!UICONTROL 身份验证]**。

   ![在[!DNL Experience Manager]](assets/analytics-insight-config.png)中为Assets Insights配置Adobe Analytics

   *图：在[!DNL Experience Manager]*&#x200B;中为Assets Insights配置Adobe Analytics

1. 成功进行身份验证后，您将在下拉列表中获得报表包。 选择您希望Assets Insights从中获取数据的Adobe Analytics **[!UICONTROL 报表包]**。 单击&#x200B;**[!UICONTROL 添加]**。

1. 在[!DNL Experience Manager]设置报表包后，单击&#x200B;**[!UICONTROL 完成]**。

有关详细信息，请参阅[Adobe Analytics Web服务](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information)。

### 页面跟踪器 {#page-tracker}

配置Adobe Analytics帐户后，将生成页面跟踪器代码。 要启用Assets Insights以跟踪第三方网站中使用的[!DNL Experience Manager]资源，请在网站代码中包含页面跟踪器代码。 使用Assets中的页面跟踪器实用程序生成页面跟踪器代码。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载页面跟踪器代码。

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
以下示例代码片段显示了示例网页中包含的页面跟踪器代码：

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
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
