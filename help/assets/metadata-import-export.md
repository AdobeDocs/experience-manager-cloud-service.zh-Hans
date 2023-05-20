---
title: 大量匯入和匯出資產中繼資料
description: 本文介紹如何大量匯入和匯出中繼資料。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 12%

---

# 大量匯入和匯出資產中繼資料 {#import-and-export-asset-metadata-in-bulk}

Adobe Experience Manager資產可讓您使用CSV檔案大量匯入資產中繼資料。 您可以匯入CSV檔案，對最近上傳的資產或現有資產執行大量更新。 您也可以以CSV格式從協力廠商系統大量擷取資產中繼資料。

## 匯入中繼資料 {#import-metadata}

中繼資料匯入為非同步處理，不會阻礙系統效能。 由於中繼資料回寫活動使用資產微服務，因此同時更新多個資產的中繼資料可能會耗費大量資源。 Adobe建議您在使用精益伺服器期間計畫任何大量作業，以免影響其他使用者的效能。

>[!NOTE]
>
>若要在自訂名稱空間上匯入中繼資料，請先註冊名稱空間。

1. 導覽至 [!DNL Assets] 使用者介面，選取 **[!UICONTROL 建立]** 從工具列中，然後選取 **[!UICONTROL 中繼資料]** 功能表中的。
1. 在 **[!UICONTROL 中繼資料匯入]** 頁面，按一下 **[!UICONTROL 選取檔案]**. 选择包含元数据的 CSV 文件。
1. 提供下列引數：

   | 参数 | 描述 |
   | ---------------------- | ------- |
   | 批量大小 | 批次中要匯入中繼資料的資產數量。 默认值为 50。最大值為100。 |
   | 字段分隔符 | 預設值為 `,` （逗號）。 您可以指定任何其他字元。 |
   | 多值分隔符號 | 中繼資料值的分隔符號。 默认值为 `|`. |
   | 启动工作流 | 預設為False。 當設定為 `true` 和預設設定對DAM中繼資料WriteBack工作流程(將中繼資料寫入二進位XMP資料)有效。 啟用工作流程會拖慢系統速度。 |
   | 资产路径列名称 | 為含有資產的CSV檔案定義欄名稱。 |

1. 選取 **[!UICONTROL 匯入]** （從工具列）。 匯入中繼資料後，系統會傳送通知至您的「通知」收件匣。 導覽至資產屬性頁面，並確認是否正確匯入資產的中繼資料值。

1. 若要新增日期和時間戳記以匯入中繼資料，請使用 `YYYY-MM-DDThh:mm:ss.fff-00:00` 日期和時間格式。 日期和時間分隔方式 `T`， `hh` 是24小時格式的小時， `fff` 為nanoseconds，且 `-00:00` 是時區位移。 例如， `2020-03-26T11:26:00.000-07:00` 為2020年3月26日的11:26:上午00:00 （太平洋標準時間）

   * 日期格式取決於欄標題及其中的格式。 例如，如果日期有格式問題 `yyyy-MM-dd'T'HH:mm:ssXXX` 則個別欄標題必須 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * 預設日期格式為 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## 导出元数据 {#export-metadata}

您可以以CSV格式匯出多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統效能。 若要匯出中繼資料，Experience Manager會周游資產節點的屬性 `jcr:content/metadata` 及其子節點，並將中繼資料屬性匯出為CSV檔案。

大量匯出中繼資料的一些使用案例包括：

* 移轉資產時，在協力廠商系統中匯入中繼資料。
* 與更廣的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料是否符合規定。
* 將中繼資料外部化，以便進行個別本地化。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 從工具列中選取 **[!UICONTROL 匯出中繼資料]**.
1. 在「中繼資料匯出」對話方塊中，指定CSV檔案的名稱。 若要匯出子資料夾中資產的中繼資料，請選取「 」 **[!UICONTROL 在子資料夾中包含資產]**.

   ![匯出資料夾中所有資產中繼資料的介面和選項](assets/export_metadata_page.png "匯出資料夾中所有資產中繼資料的介面和選項")

1. 選取所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在 **[!UICONTROL 要匯出的屬性]** 欄位中，指定您要匯出所有或特定屬性。 如果您選擇要匯出的「選擇性」屬性，請新增所需的屬性。

1. 在工具列中點選/按一下 **[!UICONTROL 匯出]**. 會出現一則訊息，確認中繼資料已匯出。 關閉訊息。
1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。要下载包含元数据的 CSV 文件，请点按/单击工具栏中的 **[!UICONTROL CSV 下载]**。单击&#x200B;**[!UICONTROL 关闭]**。

   ![用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊](assets/csv_download.png)

   *圖：用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊。*

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
>* [大量匯入資產時匯入中繼資料](/help/assets/add-assets.md#asset-bulk-ingestor)

