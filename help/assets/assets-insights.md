---
title: 资产分析
description: 跟踪在第三方网站、营销活动和Adobe的创意解决方案中使用的图像的用户评级和使用情况统计信息。
contentOwner: AG
feature: 资产分析，资产报表
role: Business Practitioner,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 1c841eaa49eeb021fc7583c58aeaefc1236650f9
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 9%

---

# 资产分析{#asset-insights}

通过Adobe分析功能，您可以跟踪用户评级以及在第三方网站、营销活动和资产创意解决方案中使用的图像的使用情况统计信息。 它有助于深入了解图像的性能和受欢迎程度。

资产分析可捕获用户活动详细信息，如图像的评级、点击次数和展示次数（图像在网站上加载的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和效果统计信息来选择要包含在目录、营销活动等中的热门图像。 您甚至可以根据这些统计数据制定存档和许可证续订策略。

要使资产分析能够从网站捕获图像的使用情况统计信息，您必须在网站代码中包含图像的嵌入代码。

要让资产分析显示资产的使用情况统计信息，请首先配置功能以从[!DNL Adobe Analytics]获取报表数据。 有关详细信息，请参阅[配置资产分析](#configure-asset-insights)。 要使用此功能，请单独购买[!DNL Adobe Analytics]许可证。

>[!NOTE]
>
>仅支持对图像提供分析。

## 查看图像{#viewing-statistics-for-an-image}的统计信息

您可以从元数据页面查看资产分析得分。

1. 从Assets用户界面中，选择图像，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]** 。
1. 在属性页面中，单击&#x200B;**[!UICONTROL 分析]**。
1. 在&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡中查看资产的使用情况详细信息。 **[!UICONTROL 分数]**&#x200B;部分描述资产的资产使用总数和性能存储。

   使用情况分数描述了资产在各种解决方案中使用的次数。

   **[!UICONTROL 展示次数]**&#x200B;分数是资产在网站上加载的次数。 在&#x200B;**[!UICONTROL Clicks]**&#x200B;下显示的数字是点击资产的次数。

1. 查看&#x200B;**[!UICONTROL 使用统计信息]**&#x200B;部分，了解资产所属的实体以及最近使用过的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **[!UICONTROL 资产]**:资产属于收藏集或复合资产的一部分的次数。
   * **[!UICONTROL Web和移动设备]**:资产成为网站和应用程序一部分的次数。
   * **[!UICONTROL 社交]**:资产在其他解决方案（如）中使用的次 [!DNL Adobe Campaign]数。
   * **[!UICONTROL 电子邮件]**:资产在电子邮件促销活动中使用的次数。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于资产分析功能通常会定期从[!DNL Adobe Analytics]中获取解决方案数据，因此解决方案部分可能不会显示最新的数据。 显示数据的时间段取决于资产分析为检索Analytics数据而运行的获取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计”部分显示最新的数据。

1. 要获取您包含在网站中的资产的嵌入代码以获取性能数据，请单击资产缩略图下方的&#x200B;**[!UICONTROL 获取嵌入代码]**。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 查看图像{#viewing-aggregate-statistics-for-images}的聚合统计信息

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在资产UI中，导航到要查看其分析的资产所在的文件夹。
1. 单击工具栏中的布局选项，然后选择&#x200B;**[!UICONTROL 分析视图]**。
1. 页面会显示资产的使用情况分数。 比较各个资产的评级并进行分析。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 配置资产分析{#configure-asset-insights}

[!DNL Experience Manager Assets] 从获取第三方网站使用的数字资产的使用情况数 [!DNL Adobe Analytics]据。要使资产分析能够检索此数据并生成分析，请首先配置该功能以与[!DNL Adobe Analytics]集成。

>[!NOTE]
>
>仅支持并提供图像分析。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的组织名称、用户名和共享密钥。

   ![在中为资产分析配置Adobe Analytics  [!DNL Experience Manager]](assets/insights_config2.png)

   *图：在中为资产分析配置Adobe Analytics[!DNL Experience Manager]*

1. 单击&#x200B;**[!UICONTROL Authenticate]**。 在[!DNL Experience Manager]验证您的凭据后，从&#x200B;**[!UICONTROL 报表包]**&#x200B;列表中，选择一个Adobe Analytics报表包，您可以从中获取资产分析数据。 单击&#x200B;**[!UICONTROL 添加]**。
1. 在[!DNL Experience Manager]设置报表包后，单击&#x200B;**[!UICONTROL 完成]**。

### 页面跟踪器{#page-tracker}

配置Adobe Analytics帐户后，将为您生成页面跟踪器代码。 要启用资产分析以跟踪第三方网站中使用的[!DNL Experience Manager]资产，请在网站代码中包含页面跟踪器代码。 在Assets中使用页面跟踪器实用程序生成页面跟踪器代码。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载页面跟踪器代码。

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
