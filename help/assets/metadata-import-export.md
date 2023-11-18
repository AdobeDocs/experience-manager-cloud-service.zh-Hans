---
title: 批量导入和导出资源元数据
description: 本文介绍了如何批量导入和导出元数据。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 10%

---

# 批量导入和导出资源元数据 {#import-and-export-asset-metadata-in-bulk}

通过Adobe Experience Manager Assets，您可以使用CSV文件批量导入资源元数据。 您可以通过导入CSV文件，对最近上传的资源或现有资源进行批量更新。 您还可以以CSV格式从第三方系统批量摄取资源元数据。

## 导入元数据 {#import-metadata}

元数据导入是异步的，不会妨碍系统性能。 由于使用资源微服务的元数据写回活动，同时更新多个资源的元数据可能会占用大量资源。 Adobe建议您在精益服务器使用期间计划任何批量操作，以免影响其他用户的性能。

>[!NOTE]
>
>要在自定义命名空间上导入元数据，请先注册命名空间。

1. 导航到 [!DNL Assets] 用户界面，选择 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 元数据]** 菜单。
1. 在 **[!UICONTROL 元数据导入]** 页面，单击 **[!UICONTROL 选择文件]**. 选择包含元数据的 CSV 文件。
1. 提供以下参数：

   | 参数 | 描述 |
   | ---------------------- | ------- |
   | 批量大小 | 要为其导入元数据的批次中的资源数。 默认值为 50。最大值为100。 |
   | 字段分隔符 | 默认值为 `,` （逗号）。 您可以指定任何其他字符。 |
   | 多值分隔符 | 元数据值的分隔符。 默认值为 `|`. |
   | 启动工作流 | 默认为False。 当设置为 `true` 和默认设置对DAM元数据回写工作流(将元数据写入二进制XMP数据)有效。 启用工作流会减慢系统速度。 |
   | 资产路径列名称 | 定义包含资产的CSV文件的列名称。 |

1. 选择 **[!UICONTROL 导入]** 工具栏中。 导入元数据后，会向您的“通知”收件箱发送通知。 导航到资源属性页面，并验证是否正确导入了资源的元数据值。

1. 要添加日期和时间戳以导入元数据，请使用 `YYYY-MM-DDThh:mm:ss.fff-00:00` 日期和时间的格式。 日期和时间由分隔 `T`， `hh` 是24小时格式的小时， `fff` 为纳秒，并且 `-00:00` 是时区偏移。 例如， `2020-03-26T11:26:00.000-07:00` 于2020年3月26日为11:26:上午00:00（太平洋标准时间）

   * 日期格式取决于列标题及其中的格式。 例如，如果日期与格式不符 `yyyy-MM-dd'T'HH:mm:ssXXX` 则相应的列标题必须 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * 默认日期格式为 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## 导出元数据 {#export-metadata}

您可以以CSV格式导出多个资源的元数据。 元数据是异步导出的，不会影响系统性能。 要导出元数据，Experience Manager将遍历资源节点的属性 `jcr:content/metadata` 及其子节点，并将元数据属性导出为CSV文件。

批量导出元数据的几个用例包括：

* 迁移资产时，在第三方系统中导入元数据。
* 与范围更广的项目团队共享资源元数据。
* 测试或审核元数据是否符合合规性。
* 将元数据外部化以便进行单独本地化。

1. 选择包含要导出元数据的资源的资源文件夹。 在工具栏中，选择 **[!UICONTROL 导出元数据]**.
1. 在“元数据导出”对话框中，指定CSV文件的名称。 要导出子文件夹中资产的元数据，请选择 **[!UICONTROL 包含子文件夹中的资源]**.

   ![用于导出文件夹中所有资源的元数据的界面和选项](assets/export_metadata_page.png "用于导出文件夹中所有资源的元数据的界面和选项")

1. 选择所需的选项。 提供文件名和（如果需要）日期。

1. 在 **[!UICONTROL 要导出的属性]** 字段，指定要导出所有属性还是特定属性。 如果您选择要导出的选择性属性，请添加所需的属性。

1. 在工具栏中，选择 **[!UICONTROL 导出]**. 将显示一条消息，确认元数据已导出。 关闭消息。
1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。要下载包含元数据的CSV文件，请选择 **[!UICONTROL CSV下载]** 工具栏中。 单击&#x200B;**[!UICONTROL 关闭]**。

   ![用于下载包含批量导出的元数据的CSV文件的对话框](assets/csv_download.png)

   *图：用于下载包含批量导出的元数据的CSV文件的对话框。*

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

>[!MORELIKETHIS]
>
>* [批量导入资产时导入元数据](/help/assets/add-assets.md#asset-bulk-ingestor)
