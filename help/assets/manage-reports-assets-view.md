---
title: 在“资源”视图中管理报告
description: 访问资源视图的报表部分中的数据，即可评估产品和功能使用情况并了解关键成功量度。
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: 6e0cd465f8695c948ece4679e083d6b9b35dded4
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 67%

---

# 管理报表 {#manage-reports}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

通过资源报表，管理员可了解Adobe Experience Manager Assets视图环境的活动。 这些数据提供关于用户如何与内容和产品进行交互的有用信息。所有用户都可以访问 Insights 仪表板，分配给管理员产品配置文件的用户可以创建用户定义的报告。

## 访问报告 {#access-reports}

所有分配给AEM管理员产品配置文件的用户均可在Assets视图中访问分析仪表板或创建用户定义的报表。

要访问报告，请导航到&#x200B;**[!UICONTROL 设置]**&#x200B;下方的&#x200B;**[!UICONTROL 报告]**。

![报告](assets/reports.png)

<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## 创建报告 {#create-report}

AEM Assets视图环境通过报表仪表板提供全面的报表功能。 这项功能使用户能够生成和下载 CSV 报告，详细记录指定时间范围内的资产上传和下载情况，从一次性到每日、每周、每月或每年。

**要创建报告，请执行以下操作：**

1. 导航到&#x200B;**报告**&#x200B;并点击&#x200B;**创建报告**（在右上角）。**创建报告**对话框会显示以下字段：
   ![创建报告](/help/assets/assets/executed-reports1.svg)

   **在“配置”选项卡中：**

   1. **报告类型：**&#x200B;从[!UICONTROL 上传]、[!UICONTROL 下载]或[Dynamic Media交付报告](#dynamic-media-delivery-reports)类型中进行选择。
   1. **标题：**&#x200B;为报告添加标题。
   1. **描述：**&#x200B;为报告添加可选描述。
   1. **选择文件夹路径：**&#x200B;选择一个文件夹路径，生成该特定文件夹内上传和下载资产的报告。例如，如果需要上传至文件夹的资产报告，请指定该文件夹的路径。
   1. **选择日期间隔：**&#x200B;选择日期范围，查看文件夹内的上传或下载活动。
   <br>

   >[!NOTE]
   >
   > 资源视图将所有本地时区转换为协调世界时 (UTC)。

   **在“列”选项卡中：**&#x200B;选择要在报告中显示的列名称。下表解释了所有列的用途：

   <table>
    <tbody>
     <tr>
      <th><strong>列名称</strong></th>
      <th><strong>描述</strong></th>
      <th><strong>报告类型</strong></th>
     </tr>
     <tr>
      <td>标题</td>
      <td>资产的标题。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>路径</td>
      <td>在资源视图中可从中找到资源的文件夹路径。</td>
      <td>上传、下载和Dynamic Media交付</td>
     </tr>
     <tr>
      <td>MIME 类型</td>
      <td>资产的 MIME 类型。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>资产的大小，以字节为单位。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>下载者</td>
      <td>下载资产的用户的电子邮件 ID。</td>
      <td>下载</td>
     </tr>
     <tr>
      <td>下载日期</td>
      <td>执行资产下载操作的日期。</td>
      <td>下载</td>
     </tr>
     <tr>
      <td>创作</td>
      <td>资产的作者。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>创建日期</td>
      <td>将资源上传到资源视图的日期。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改资产的日期。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>到期</td>
      <td>资产的到期状态。</td>
      <td>上传和下载</td>
     </tr>
     <tr>
      <td>下载者用户名</td>
      <td>下载资产的用户的名称。</td>
      <td>下载</td>
     </tr> 
     <tr>
      <td>引用</td>
      <td>交付或包含资产的URL</td>
      <td>Dynamic Media 投放</td>
     </tr>  
     <tr>
      <td>点击量</td>
      <td>交付资产的次数（投放计数）</td>
      <td>Dynamic Media 投放</td>
     </tr>          
    </tbody>
   </table>

## Dynamic Media投放报告 {#dynamic-media-delivery-reports}

获取通过 Dynamic Media 投放资产的投放洞察，包括资产级别投放计数、推荐人信息、AEM Assets 中的资产路径和唯一资产 ID。可以为AEM Assets存储库中通过Dynamic Media交付的所有资源或AEM Assets中的特定文件夹层次结构生成报表。 此外，Dynamic Media交付报表分析有助于衡量所交付资产的ROI、衡量渠道绩效并帮助执行针对资产的明智资源管理任务。

>[!NOTE]
> 
>若要提前访问您Dynamic Media帐户的Dynamic Media交付报告，请[创建并提交Adobe的客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。

### 先决条件 {#prereqs-dynamic-media-delivery-reports}

您应该具有Dynamic Media许可证才能创建并使用此报表。

>[!IMPORTANT]
> 
>* 提供通过动态媒体投放的资产的报告。
>* 报告针对前 100 万行生成。要捕获此限制内的所有文件，请考虑为较小的文件夹添加引荐来源列。
>* 仅可生成过去 3 个月的报告。

### 创建Dynamic Media投放报告{#create-dynamic-media-delivery-report}

1. 使用[创建报告](#create-report)中所述的步骤创建Dynamic Media投放报告。

1. 从&#x200B;**[!UICONTROL 报告类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Dynamic Media投放]**。

   ![Dynamic Media投放报告下拉列表](assets/dynamic-media-delivery-report-option.png)


1. 在&#x200B;**[!UICONTROL 列]**&#x200B;选项卡中，您可以选择&#x200B;**[!UICONTROL 反向链接]**&#x200B;列以将其包含在您的报表中。

   ![反向链接](assets/referrer.png)

   下载的报表的所有列都是只读的，但&#x200B;**反向链接**&#x200B;列除外，您可以将其修改为包含或排除在此报表中。<!--Choosing a referrer displays the number of visitors received from each referred report that directs traffic to the site. It offers insights into the sources of traffic and the origin of the visitors. Such insights help measure ROI of delivered assets, measure channel performance, and help take informed asset management tasks for assets.-->

### 对Dynamic Media投放报告执行的操作 {#actions-performed-dynamic-media-delivery-reports}

创建报告后，您可以执行以下操作：

* **[!UICONTROL 删除]**：您可以删除所选的报告。
* **[!UICONTROL 下载CSV]**：您可以以CSV格式下载选定的报表。 下载的报表包含名称、路径、DynamicMediaID、反向链接、点击量列。
   * **反向链接**&#x200B;列列出了交付或包含资产的URL。

   * **点击**&#x200B;列列出了交付资产的次数（投放计数）。

要删除或下载CSV格式的Dynamic Media交付报表，请参阅[查看和下载现有报表](#View-and-download-existing-report)。

![已下载Dynamic Media投放报告中的CSV](assets/csv-dynamic-media-delivery-report.png)


## 查看和下载现有报告 {#View-and-download-existing-report}

现有报告显示在&#x200B;**已执行报告** 选项卡下。点击&#x200B;**报告**&#x200B;并选择&#x200B;**已执行报告**&#x200B;可查看所有已创建的报告，其状态为&#x200B;**已完成**，表示这些报告可随时下载。要以 CSV 格式下载报告或删除报告，请选择报告行。然后选择&#x200B;**下载 CSV**&#x200B;或&#x200B;**删除**。![查看和下载现有报告](/help/assets/assets/view-download-existing-report.png)


## 计划一份报告 {#schedule-report}

在AEM Assets视图UI中，**计划报表**&#x200B;设置按指定的未来时间间隔（如每日、每周、每月或每年）自动生成报表。 此功能有助于简化定期报告需求并确保及时更新数据。**创建报告**&#x200B;会生成过去日期的报告。已完成的报告列于&#x200B;**已执行报告**&#x200B;下，即将生成的报告列于&#x200B;**计划报告**&#x200B;下。

要计划一份报告，请按照以下步骤操作：

1. 点击左侧窗格中的“报告”，然后点击“创建报告”（在右上角）。
1. 报告对话框会显示以下信息：
   1. **报告类型：**&#x200B;选择上传或下载类型。
   1. **标题：**&#x200B;为报告添加标题。
   1. **描述**：为报告添加可选描述。
   1. **选择文件夹路径：**&#x200B;选择一个文件夹路径，为将来上传到该特定文件夹或从该文件夹下载的资产生成报告。
   1. 切换&#x200B;**计划报告：**切换以将报告安排到稍后时间或重复出现。
      ![计划报告](/help/assets/assets/schedule-reports1.svg)

   1. **选择频率：**&#x200B;指定生成报告的时间间隔（例如，每天、每周、每月、每年或一次），并设置运行报告的日期和时间以及重复出现的结束日期。对于一次性报告，请选择 AEM 环境中所选活动类型的报告的日期范围。例如，如果需要某月 10 日至 29 日（未来日期）的下载资产报告，请在&#x200B;**选择日期间隔**&#x200B;字段中选择这些日期。

   >[!NOTE]
   >
   > 资源视图将所有本地时区转换为协调世界时 (UTC)。

## 查看计划报告 {#view-scheduled-reports}

计划报告以系统组织的方式在&#x200B;**计划报告**&#x200B;选项卡下显示。每个计划报告的所有已完成报告都存储在一个报告文件夹中。单击![展开折叠](/help/assets/assets/expand-icon1.svg)以查看已完成的报告。 例如，如果您安排了每日报告，所有已完成的报告都会分组放在一个文件夹中。这种组织方式简化了报告的导航和查找。要查看计划报告，请点击&#x200B;**报告**，然后点击&#x200B;**计划报告**。所有的计划报告状态都会显示为进行中或已完成。已完成的报告可供下载。\
![计划报告](/help/assets/assets/scheduled-reports-tab.png)

## 编辑和取消计划报告 {#edit-cancel-scheduled-reports}

1. 导航至&#x200B;**计划报告**&#x200B;选项卡。
1. 选择报告行。
1. 点击&#x200B;**编辑**。
1. 点击&#x200B;**取消计划**，然后点击&#x200B;**确认**，即可取消计划报告。对于已取消的报告，下一次运行时间将变为空，状态显示为已取消。
   ![编辑和取消计划报告](/help/assets/assets/cancel-edit-scheduled-reports.png)

### 恢复计划 {#resume-schedule}

要恢复已取消的计划，请选择报告行并点击&#x200B;**恢复计划**。恢复后，将再次显示下一个运行时间条目，状态显示为进行中。
![恢复计划](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> 如果在计划结束日期前恢复已取消的报告，则会自动生成从取消日期到恢复日期的报告。

## 查看见解 {#view-live-statistics}

通过资源视图的“见解”仪表板，可查看资源视图环境的实时数据。可查看过去 30 天或过去 12 个月的实时事件指标。

<!--![Toolbar options when you select an asset](assets/assets-view-live-statistics.png)-->

单击可在左侧导航窗格中找到的&#x200B;**[!UICONTROL 见解]**&#x200B;以查看以下自动生成的图表：

* **下载**：过去30天或12个月从Assets视图环境下载的资源数量，用折线图表示。
  ![分析 — 下载](/help/assets/assets/insights-downloads2341.svg)

* **上传**：过去30天或12个月内上传到Assets视图环境的资源数，用折线图表示。
  ![分析 — 上载](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **存储使用情况**：使用条形图表示的Assets视图环境的存储使用情况（以字节为单位）。
  ![分析 — 上载](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **热门搜索**：以表格格式查看过去 30 天或 12 个月内在资源视图环境中搜索最多的术语以及这些术语的搜索次数。
  ![分析 — 上载](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->
* **按大小进行资源计数：** 将资源视图环境中的总资源数量细分为不同的大小范围，突出显示每个大小范围内的资源数量和百分比，以环形图表示。
  ![洞察资源按大小计数](/help/assets/assets/insights-assets-count-by-size.svg)
* 按资源类型划分的&#x200B;**资源计数：**在Assets视图环境中对资源总数进行分段，根据资源文件类型突出显示资源的计数和百分比，用圆环图表示。
  ![洞察按规模统计资产数量](/help/assets/assets/insights-assest-count-by-asset-type1.svg)