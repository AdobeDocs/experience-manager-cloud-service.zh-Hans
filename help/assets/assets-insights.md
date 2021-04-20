---
title: 资产分析
description: 跟踪在第三方网站、营销活动和Adobe的创意解决方案中使用的图像的用户评级和使用统计信息。
contentOwner: AG
feature: 资产分析，资产报表
role: Business Practitioner
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
translation-type: tm+mt
source-git-commit: a42138cd009a85a92e74d98dd808578014361e1d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 10%

---

# 资产分析 {#asset-insights}

资产分析跟踪在第三方网站、营销活动和Adobe的创意解决方案中使用的图像的用户评级和使用统计信息。 它有助于提供有关图像性能和受欢迎程度的洞察。

资产分析可捕获用户活动详细信息，例如对图像进行评级、单击和展示次数（在网站上加载图像的次数）。 它根据这些统计信息为图像分配分数。 您可以使用分数和性能统计信息来选择热门图像，以将其纳入目录、营销活动等。 您甚至可以根据这些统计数据制定存档和许可证续订策略。

要使资产分析能够从网站捕获图像的使用情况统计信息，您必须在网站代码中包含图像的嵌入代码。

要让资产分析显示资产的使用情况统计信息，请首先配置该功能以从Adobe Analytics获取报告数据。 有关详细信息，请参阅[配置资产分析](#configure-asset-insights)。

>[!NOTE]
>
>只支持并提供图像分析。

## 图像{#viewing-statistics-for-an-image}的视图统计

您可以从元数据页面视图资产分析分数。

1. 从资产用户界面(UI)中，选择图像，然后点按工具栏中的&#x200B;**[!UICONTROL 属性]**。
1. 在“属性”页中，点按&#x200B;**[!UICONTROL Insights]**。
1. 在&#x200B;**[!UICONTROL Insights]**&#x200B;选项卡中查看资产的使用详细信息。 **[!UICONTROL Score]**&#x200B;部分描述资产的资产使用总数和性能存储。

   使用情况分数描述资产在各种解决方案中的使用次数。

   **[!UICONTROL 展示次数]**&#x200B;分数是资产在网站上加载的次数。 **[!UICONTROL 单击]**&#x200B;下显示的数字是单击资产的次数。

1. 查看&#x200B;**[!UICONTROL 使用统计信息]**&#x200B;部分，了解资产所属的实体以及最近使用的创意解决方案。 使用率越高，该资产在用户中受欢迎的可能性就越大。 使用数据显示在以下标题下：

   * **[!UICONTROL 资产]**:资产属于集合或复合资产的次数。
   * **[!UICONTROL Web和移动]**:资产加入网站和应用程序的次数。
   * **[!UICONTROL 社交]**:资产在解决方案(如Adobe Social和Adobe Campaign)中的使用次数。
   * **[!UICONTROL 电子邮件]**:资产在电子邮件活动中的使用次数。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于资产分析功能通常会定期从Adobe Analytics获取解决方案数据，因此解决方案部分可能不会显示最新数据。 显示数据的时间段取决于资产分析运行以检索Analytics数据的提取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计”部分显示最新数据。

1. 要获取包含在网站中的资产的嵌入代码以获取性能数据，请点按/单击资产缩略图下方的&#x200B;**[!UICONTROL 获取嵌入代码]**。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 图像{#viewing-aggregate-statistics-for-images}的视图聚合统计信息

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在资产用户界面中，导航到包含要视图分析的资产的文件夹。
1. 点按/单击工具栏中的布局图标，然后选择&#x200B;**[!UICONTROL 分析视图]**。
1. 该页面显示资产的使用分数。 比较各个资产的评级并进行分析。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 配置资产分析{#configure-asset-insights}

[!DNL Experience Manager Assets] 从中获取第三方网站使用的数字资产的使用数据 [!DNL Adobe Analytics]要使资产分析能够检索此数据并生成洞察，请首先配置该功能以与[!DNL Adobe Analytics]集成。

>[!NOTE]
>
>只支持并提供图像分析。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的单位名称、用户名和共享机密。

   ![在中为资产分析配置Adobe Analytics  [!DNL Experience Manager]](assets/insights_config2.png)

   *图：在中为资产分析配置Adobe Analytics[!DNL Experience Manager]*

1. 单击／点按 **[!UICONTROL 身份验证]**。在[!DNL Experience Manager]验证您的凭据后，从&#x200B;**[!UICONTROL 报表包]**&#x200B;列表中，选择Adobe Analytics报表包，您希望资产分析从中获取数据。 单击&#x200B;**[!UICONTROL 添加]**。
1. 在[!DNL Experience Manager]设置报表包后，点按&#x200B;**[!UICONTROL 完成]**。

### 页面跟踪器{#page-tracker}

配置Adobe Analytics帐户后，将为您生成页面跟踪器代码。 要使资产分析能够跟踪第三方网站中使用的[!DNL Experience Manager]资产，请在网站代码中包含页面跟踪器代码。 使用资产中的页面跟踪器实用程序生成页面跟踪器代码。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载页面跟踪器代码。

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
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
