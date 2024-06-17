---
title: 有关使用和共享的报告
description: 有关您在中资源的报表 [!DNL Adobe Experience Manager Assets] 以帮助您了解数字资产的使用、活动和共享。
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 9%

---

# 资源报告 {#asset-reports}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service | 本文 |

通过资产报告，您可以评估 [!DNL Adobe Experience Manager Assets] 部署。 替换为 [!DNL Assets]，您可以为数字资源生成各种报表。 这些报表提供有关系统使用情况、用户与资源的交互方式以及哪些资源的有用信息 <!-- downloaded and --> 共享。

使用报告中的信息获得关键成功指标以衡量采用情况 [!DNL Assets] 企业内部和客户。

此 [!DNL Assets] 报告框架使用 [!DNL Sling] 作业，用于按顺序异步处理报表请求。 它可扩展到大型存储库。 异步报表处理提高了生成报表的效率和速度。

报告管理界面非常直观，包括细粒度选项和控件，可用于访问存档的报告和查看报告运行状态（成功、失败和排队）。

生成报告时，系统会通过以下方式通知您 <!-- through an email (optional) and --> 收件箱通知。 您可以在显示之前生成的所有报表的报表列表页面中查看、下载或删除报表。

## 生成报表 {#generate-reports}

[!DNL Experience Manager Assets] 会为您生成以下标准报表：

* 上传
* 下载
* 到期时间
* 修改
* 发布
* [!DNL Brand Portal] 发布
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

[!DNL Adobe Experience Manager] 管理员可以轻松地为您的实施生成和自定义这些报表。 管理员可以按照以下步骤生成报告：

1. 在 [!DNL Experience Manager] 界面，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.

   ![用于导航资产报表的“工具”页面](assets/navigation.png)

1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 工具栏中。
1. 从 **[!UICONTROL 创建报告]** 页面上，选择要创建的报表，然后单击 **[!UICONTROL 下一个]**.

   ![选择报表类型](assets/choose_report.png)

1. 配置报表详细信息，如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为 `/content/dam`. 您可以指定其他路径在特定文件夹上执行报告。

   ![用于添加报告详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。 您可以选择立即生成报表，也可以选择在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在日期和时间字段中指定日期和时间。 如果您未指定任何值，则报告引擎会将其视为将立即生成的报告。

   根据您创建的报告类型，配置字段可能会有所不同。 例如， **[!UICONTROL 磁盘使用情况]** 报表提供了一些选项，用于在计算资产使用的磁盘空间时包含资产演绎版。 您可以选择在子文件夹中包括或排除资产以计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   ![“磁盘使用情况”报告的“详细信息”页面](assets/disk_usage_configuration.png)

   当您创建 **[!UICONTROL 文件]** 报表中，您可以包含/排除子文件夹。 但是，您不能包含此报表的资产演绎版。

   ![“文件”报告的“详细信息”页面](assets/files_report.png)

   此 **[!UICONTROL 链接共享]** 报表显示从内与外部用户共享的资产的URL [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> 列不可自定义。

   此 **[!UICONTROL 链接共享]** 报表中，不包括子文件夹和呈现形式的选项，因为它仅发布显示在下的共享URL `/var/dam/share`.

   ![链接共享报告的详细信息页面](assets/link_share.png)

1. 单击 **[!UICONTROL 下一个]** 工具栏中。

1. 在 **[!UICONTROL 配置列]** 页面，默认情况下会选择在报表中显示的某些列。 您可以选择更多列。 取消选择要在报表中排除它的列。

   ![选择或取消选择报表列](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在 `jcr:content` CRX中的节点。 或者，通过属性路径选取器添加它。

   ![选择或取消选择报表列](assets/custom_columns.png)

1. 单击 **[!UICONTROL 创建]** 工具栏中。 此时将显示一条消息，通知已启动报表生成。
1. 在 [!UICONTROL 资产报表] 页面上，报表生成状态基于报表作业的当前状态，例如， [!UICONTROL 成功]， [!UICONTROL 失败]， [!UICONTROL 已排队]，或 [!UICONTROL 已计划]. 通知收件箱中将显示相同的状态。要查看报告页面，请单击报告链接。 或者，选择报告，然后单击 **[!UICONTROL 视图]** 工具栏中。

   <!--![A generated report](assets/report_page.png)-->
   ![已生成报告状态](assets/report-status.JPG)

   单击 **[!UICONTROL 下载]** 从工具栏以CSV格式下载报表。

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
* 到期时间
* 修改
* 发布
* [!DNL Brand Portal] 发布
* 文件

要向这些报表中添加自定义列，请执行以下步骤：

1. 在 [!DNL Manager interface]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.
1. 在 [!UICONTROL 资产报表] 页面，单击 **[!UICONTROL 创建]** 工具栏中。

1. 从 **[!UICONTROL 创建报告]** 页面上，选择要创建的报告。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 根据需要配置报表详细信息，如标题、描述、缩略图、文件夹路径和日期范围。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 从列表中选择适用的信息 **[!UICONTROL 默认列]**. 要显示自定义列，请指定下方的列的名称 **[!UICONTROL 自定义列]**.

   ![指定报表自定义列的名称](assets/custom_columns-1.png)

1. 将属性路径添加到 `jcr:content` CRXDE中的节点。 或者，在属性路径字段中键入路径。

   ![从jcr：content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单击 **[!UICONTROL 添加]** 并重复上述步骤。

1. 单击 **[!UICONTROL 创建]** 工具栏中。 此时将显示一条消息，通知已启动报表生成。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## 疑难解答信息 {#tips-troubleshoot}

* 如果 [!UICONTROL 磁盘使用情况报表] 不会生成，如果您使用 [!DNL Dynamic Media]，确保正确处理所有资源。 要解决此问题，请重新处理资源并再次生成报表。

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
