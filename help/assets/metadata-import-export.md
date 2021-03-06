---
title: 批量导入和导出资产元数据
description: 本文介绍了如何批量导入和导出元数据。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: ce7ba090a97c2f265af8ed21f11a5a45880e010a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 9%

---

# 批量导入和导出资产元数据 {#import-and-export-asset-metadata-in-bulk}

Adobe Experience Manager Assets允许您使用CSV文件批量导入资产元数据。 您可以通过导入CSV文件，对最近上传的资产或现有资产进行批量更新。 您还可以以CSV格式从第三方系统批量摄取资产元数据。

## 导入元数据 {#import-metadata}

元数据导入是异步的，不会影响系统性能。 由于使用资产微服务执行元数据写回活动，因此同时更新多个资产的元数据可能会占用大量资源。 Adobe建议您规划精益服务器使用期间的任何批量操作，以便不会影响其他用户的性能。

>[!NOTE]
>
>要导入自定义命名空间的元数据，请首先注册命名空间。

1. 导航到 [!DNL Assets] 用户界面，选择 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 元数据]** 中。
1. 在 **[!UICONTROL 元数据导入]** 页面，单击 **[!UICONTROL 选择文件]**. 选择包含元数据的 CSV 文件。
1. 提供以下参数：

   | 参数 | 描述 |
   | ---------------------- | ------- |
   | 批量大小 | 要为其导入元数据的批次中的资产数量。 默认值为 50。最大值为100。 |
   | 字段分隔符 | 默认值为 `,` （逗号）。 您可以指定任何其他字符。 |
   | 多值分隔符 | 元数据值的分隔符。 默认值为 `|`. |
   | 启动工作流 | 默认为False。 当设置为 `true` 和默认设置对DAM元数据回写工作流(将元数据写入二进制XMP数据)有效。 启用工作流会减慢系统速度。 |
   | 资产路径列名称 | 为包含资产的CSV文件定义列名称。 |

1. 选择 **[!UICONTROL 导入]** 中。 导入元数据后，系统会向您的通知收件箱发送通知。 导航到资产属性页面，并验证是否为资产正确导入了元数据值。

1. 要添加日期和时间戳以导入元数据，请使用 `YYYY-MM-DDThh:mm:ss.fff-00:00` 日期和时间的格式。 日期和时间以 `T`, `hh` 是24小时格式， `fff` 为纳秒，并且 `-00:00` 是时区偏移。 例如， `2020-03-26T11:26:00.000-07:00` 于2020年3月26日11时:26:上午00点（太平洋标准时间）。

   * 日期格式取决于列标题及其格式。 例如，如果日期是带有格式的投诉 `yyyy-MM-dd'T'HH:mm:ssXXX` 则相应的列标题必须为 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * 默认日期格式为 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## 导出元数据 {#export-metadata}

您可以以CSV格式导出多个资产的元数据。 元数据是异步导出的，不会影响系统性能。 要导出元数据，Experience Manager会遍历资产节点的属性 `jcr:content/metadata` 及其子节点，并将元数据属性导出为CSV文件。

批量导出元数据的一些用例包括：

* 迁移资产时，在第三方系统中导入元数据。
* 与更广的项目团队共享资产元数据。
* 测试或审核元数据以确保合规性。
* 将元数据外部化以实现单独的本地化。

1. 选择包含要导出元数据的资产的资产文件夹。 在工具栏中，选择 **[!UICONTROL 导出元数据]**.
1. 在元数据导出对话框中，指定CSV文件的名称。 要导出子文件夹中资产的元数据，请选择 **[!UICONTROL 在子文件夹中包含资产]**.

   ![用于导出文件夹中所有资产的元数据的界面和选项](assets/export_metadata_page.png "用于导出文件夹中所有资产的元数据的界面和选项")

1. 选择所需的选项。 提供文件名，并在必要时提供日期。

1. 在 **[!UICONTROL 要导出的属性]** 字段中，指定要导出全部属性还是特定属性。 如果选择要导出的选择性属性，请添加所需的属性。

1. 在工具栏中，点按/单击 **[!UICONTROL 导出]**. 系统会显示一条消息，确认已导出元数据。 关闭消息。
1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。要下载包含元数据的 CSV 文件，请点按/单击工具栏中的 **[!UICONTROL CSV 下载]**。单击&#x200B;**[!UICONTROL 关闭]**。

   ![用于下载包含批量导出元数据的CSV文件的对话框](assets/csv_download.png)

   *图：用于下载包含批量导出元数据的CSV文件的对话框。*

>[!MORELIKETHIS]
>
>* [批量导入资产时导入元数据](/help/assets/add-assets.md#asset-bulk-ingestor)

