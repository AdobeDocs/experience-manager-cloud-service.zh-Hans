---
title: 在“资产”视图中管理报表
description: 访问Assets视图的报表部分中的数据，以评估产品和功能使用情况，并得出有关关键成功指标的见解。
exl-id: c7155459-05d9-4a95-a91f-a1fa6ae9d9a4
source-git-commit: df82681338f8ca1a34df6118cbddc6642aa8d4b5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 71%

---

# 管理报表 {#manage-reports}

>[!CONTEXTUALHELP]
>id="assets_reports"
>title="报表"
>abstract="通过资源报表，管理员可了解Adobe Experience Manager Assets视图环境的活动。 这些数据提供关于用户如何与内容和产品进行交互的有用信息。所有分配给管理员产品配置文件的用户均可访问 Insights 仪表板或创建用户定义的报表。"

通过资源报表，管理员可了解Adobe Experience Manager Assets视图环境的活动。 这些数据提供关于用户如何与内容和产品进行交互的有用信息。

## 访问报表 {#access-reports}

所有分配给Assets视图管理员产品配置文件的用户均可在Assets视图中访问Insights仪表板或创建用户定义的报表。

## 查看见解 {#view-live-statistics}

通过“资产”视图，您可以使用“分析”仪表板查看“资产”视图环境的实时数据。 可查看过去 30 天或过去 12 个月的实时事件指标。

![选择资源后出现的工具栏选项](assets/assets-essentials-live-statistics.png)

单击可在左侧导航窗格中找到的&#x200B;**[!UICONTROL 见解]**&#x200B;以查看以下自动生成的图表：

* **下载**：使用折线图表示过去30天或12个月内从资源视图环境下载的资源数。

* **上传**：使用折线图表示过去30天或12个月内上传到Assets视图环境的资产数量。

* **热门搜索**：以表格格式查看过去30天或12个月内Assets视图环境中排名最前的搜索词以及这些搜索词的搜索次数。

<!--

* **Storage usage**: The storage usage, in gigabytes (GB), for the Assets view environment, for the last 30 days or 12 months represented using a bar chart.

-->

## 创建下载报告 {#create-download-report}

要创建下载报告：

1. 请导航到&#x200B;**[!UICONTROL “设置”]**>**[!UICONTROL “报告”]**，然后单击&#x200B;**[!UICONTROL “创建报告”]**。

1. 在[!UICONTROL 配置]选项卡中，将报告类型指定为&#x200B;**[!UICONTROL 下载]**。

1. 指定报告的标题和可选描述。

1. 使用&#x200B;**[!UICONTROL 选择文件夹路径]**&#x200B;字段选择文件夹路径，其中包括要对其执行报表的资源。

1. 选择该报表的日期间隔。

   >[!NOTE]
   >
   > 资产视图将所有本地时区转换为协调世界时(UTC)。

1. 在[!UICONTROL 列]选项卡中，选择需要在该报表中显示的列名称。

1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![下载报表](assets/download-reports-config.png)

下表阐述所有可添加到该报表的列的用途：

<table>
    <tbody>
     <tr>
      <th><strong>列名称</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>标题</td>
      <td>资源的标题。</td>
     </tr>
     <tr>
      <td>路径</td>
      <td>资产在“资产”视图中可用的文件夹路径。</td>
     </tr>
     <tr>
      <td>MIME 类型</td>
      <td>资源的 MIME 类型。</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>资源的大小，以字节为单位。</td>
     </tr>
     <tr>
      <td>下载者</td>
      <td>下载资源的用户的电子邮件 ID。</td>
     </tr>
     <tr>
      <td>下载日期</td>
      <td>执行资源下载操作的日期。</td>
     </tr>
     <tr>
      <td>创作</td>
      <td>资源的作者。</td>
     </tr>
     <tr>
      <td>创建日期</td>
      <td>将资产上传到“资产”视图的日期。</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改资源的日期。</td>
     </tr>
     <tr>
      <td>到期</td>
      <td>资源的到期状态。</td>
     </tr>
     <tr>
      <td>下载者用户名</td>
      <td>下载资源的用户的名称。</td>
     </tr>           
    </tbody>
   </table>

## 创建上载报告 {#create-upload-report}

要创建上载报告：

1. 请导航到&#x200B;**[!UICONTROL “设置”]**>**[!UICONTROL “报告”]**，然后单击&#x200B;**[!UICONTROL “创建报告”]**。

1. 在[!UICONTROL 配置]选项卡中，将报告类型指定为&#x200B;**[!UICONTROL 上载]**。

1. 指定报告的标题和可选描述。

1. 使用&#x200B;**[!UICONTROL 选择文件夹路径]**&#x200B;字段选择文件夹路径，其中包括要对其执行报表的资源。

1. 选择该报表的日期间隔。

1. 在[!UICONTROL 列]选项卡中，选择需要在该报表中显示的列名称。

1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![上载报告](assets/upload-reports-config.png)

下表阐述所有可添加到该报表的列的用途：

<table>
    <tbody>
     <tr>
      <th><strong>列名称</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>标题</td>
      <td>资源的标题。</td>
     </tr>
     <tr>
      <td>路径</td>
      <td>资产在“资产”视图中可用的文件夹路径。</td>
     </tr>
     <tr>
      <td>MIME 类型</td>
      <td>资源的 MIME 类型。</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>资源的大小。</td>
     </tr>
     <tr>
      <td>创作</td>
      <td>资源的作者。</td>
     </tr>
     <tr>
      <td>创建日期</td>
      <td>将资产上传到“资产”视图的日期。</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改资源的日期。</td>
     </tr>
     <tr>
      <td>到期</td>
      <td>资源的到期状态。</td>
     </tr>              
    </tbody>
   </table>

## 查看现有报表 {#view-report-list}

在[创建报告](#create-download-report)之后，可查看现有报表的列表，然后选择以 CSV 格式下载报表或删除报表。

要查看报表的列表，请导航至&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 报表]**。

对于每个报表，均可查看报表标题、报表类型、创建报表时指定的描述、报表状态、创建报表的作者的电子邮件 ID 和报表创建日期。

报表的 `Completed ` 状态表示报表准备就绪，可供下载。

![报表的列表](assets/list-of-reports.png)


## 下载 CSV 报表 {#download-csv-report}

要以 CSV 格式下载报表，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 报表]**。

1. 选择一个报表，然后单击&#x200B;**[!UICONTROL 下载 CSV]**。

随后将以 CSV 格式下载所选的报表。在 CSV 报表中显示的列取决于在[创建报表](#create-download-report)时选择的列。

## 删除报表 {#delete-report}

要删除报表，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 报表]**。

1. 选择一个报表，然后单击&#x200B;**[!UICONTROL 删除]**。

1. 再次单击&#x200B;**[!UICONTROL 删除]**&#x200B;以确认。
