---
title: 有关使用和共享的报告
description: 有关 [!DNL Adobe Experience Manager Assets] 中您的资产的报告，可帮助您了解数字资产的使用情况、活动和共享。
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 6a03eb1a4ac8284299c1ffcf27d6a6c8a8b9abc4
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 10%

---

# 资源报告 {#asset-reports}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service | 本文 |

通过资产报告，您可以评估[!DNL Adobe Experience Manager Assets]部署的实用程序。 通过[!DNL Assets]，您可以为数字资源生成各种报告。 这些报表提供有关系统使用情况、用户如何与资源交互以及<!-- downloaded and -->共享哪些资源的有用信息。

使用报告中的信息获得关键成功指标以衡量在您的企业内和客户采用[!DNL Assets]的情况。

[!DNL Assets]报告框架异步使用[!DNL Sling]作业按顺序处理报告请求。 它可扩展到大型存储库。 异步报表处理提高了生成报表的效率和速度。

报告管理界面非常直观，包括细粒度选项和控件，可用于访问存档的报告和查看报告运行状态（成功、失败和排队）。

在生成报告时，您会通过<!-- through an email (optional) and -->收到收件箱通知。 您可以在显示之前生成的所有报表的报表列表页面中查看、下载或删除报表。

## 生成报表 {#generate-reports}

[!DNL Experience Manager Assets]为您生成以下标准报告：

* 上传
* 下载
* 期限
* 修改
* 发布
* [!DNL Brand Portal]发布
* 磁盘使用情况
* 文件
* 链接共享

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager]管理员可以轻松地为您的实施生成和自定义这些报表。 管理员可以按照以下步骤生成报告：

1. 在[!DNL Experience Manager]界面中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 报表]**。

   ![用于导航资产报表的“工具”页面](assets/navigation.png)

1. 在[!UICONTROL 资产报表]页面上，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。
1. 从&#x200B;**[!UICONTROL 创建报告]**&#x200B;页面中，选择要创建的报告，然后单击&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >使自己有权使用&#x200B;**AEM管理员产品配置文件**&#x200B;来创建&#x200B;**下载**&#x200B;报告。 请参阅[分配AEM产品配置文件](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem)，以授予您使用AEM管理员产品配置文件的权限。

   ![选择报表类型](assets/choose_report.png)

1. 配置报表详细信息，如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为`/content/dam`。 您可以指定其他路径在特定文件夹上执行报告。

   ![添加报告详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。 您可以选择立即生成报表，也可以选择在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在日期和时间字段中指定日期和时间。 如果您未指定任何值，则报告引擎会将其视为将立即生成的报告。

   根据您创建的报告类型，配置字段可能会有所不同。 例如，**[!UICONTROL 磁盘使用情况]**&#x200B;报表提供了选项，以便在计算资源使用的磁盘空间时包含资源演绎版。 您可以选择在子文件夹中包括或排除资产以计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   磁盘使用情况报告的![详细信息页面](assets/disk_usage_configuration.png)

   创建&#x200B;**[!UICONTROL 文件]**&#x200B;报告时，您可以包含/排除子文件夹。 但是，您不能包含此报表的资产演绎版。

   ![文件报告的详细信息页面](assets/files_report.png)

   **[!UICONTROL 链接共享]**&#x200B;报表显示从[!DNL Assets]内与外部用户共享的资产的URL。 <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. -->列不可自定义。

   **[!UICONTROL 链接共享]**&#x200B;报告不包含子文件夹和呈现形式的选项，因为它仅发布显示在`/var/dam/share`下的共享URL。

   链接共享报告的![详细信息页面](assets/link_share.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 配置列]**&#x200B;页中，默认情况下选择报表中显示的某些列。 您可以选择更多列。 取消选择要在报表中排除它的列。

   ![选择或取消选择报表列](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在CRX中的`jcr:content`节点下配置资产二进制文件的属性。 或者，通过属性路径选取器添加它。

   ![选择或取消选择报表列](assets/custom_columns.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 创建]**。 此时将显示一条消息，通知已启动报表生成。
1. 在[!UICONTROL 资产报表]页面上，报表生成状态基于报表作业的当前状态，例如[!UICONTROL 成功]、[!UICONTROL 失败]、[!UICONTROL 已排队]或[!UICONTROL 已计划]。 通知收件箱中将显示相同的状态。 要查看报表页面，请单击报表链接。 或者，选择报告，然后单击工具栏中的&#x200B;**[!UICONTROL 查看]**。

   <!--![A generated report](assets/report_page.png)-->
   ![已生成报告状态](assets/report-status.JPG)

   单击工具栏中的&#x200B;**[!UICONTROL 下载]**&#x200B;以CSV格式下载报表。

   >[!NOTE]
   >
   >您可以根据过去360天内生成的事件生成报告。 Experience Manager会将用户ID数据保留30天。

## 向报表添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以显示更多符合自定义要求的数据：

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* 上传
* 期限
* 修改
* 发布
* [!DNL Brand Portal]发布
* 文件

要向这些报表中添加自定义列，请执行以下步骤：

1. 在[!DNL Manager interface]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 报表]**。
1. 在[!UICONTROL 资产报表]页面上，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。

1. 从&#x200B;**[!UICONTROL 创建报告]**&#x200B;页面中，选择要创建的报告。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 根据需要配置报表详细信息，如标题、描述、缩略图、文件夹路径和日期范围。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 从&#x200B;**[!UICONTROL 默认列]**&#x200B;列表中选择适用的信息。 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![为报告的自定义列指定名称](assets/custom_columns-1.png)

1. 使用属性路径选取器在CRXDE中的`jcr:content`节点下添加属性路径。 或者，在属性路径字段中键入路径。

   ![从jcr：content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单击“添加”****&#x200B;并重复上述步骤。

1. 单击工具栏中的&#x200B;**[!UICONTROL 创建]**。 此时将显示一条消息，通知已启动报表生成。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## 疑难解答信息 {#tips-troubleshoot}

* 如果[!UICONTROL 磁盘使用情况报表]未生成，并且您使用的是[!DNL Dynamic Media]，请确保正确处理所有资源。 要解决此问题，请重新处理资源并再次生成报表。

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
