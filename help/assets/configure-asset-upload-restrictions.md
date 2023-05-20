---
title: 配置资源上传限制
description: 設定Adobe Experience Manager資產，根據MIME型別限制使用者可上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 12%

---

# 配置资源上传限制 {#configure-asset-upload-restrictions}

您可以設定Adobe Experience Manager資產，根據MIME型別限制使用者可上傳的資產型別。

>[!IMPORTANT]
>
>依預設，Experience Manager Assets可讓使用者上傳所有MIME型別的資產。 不過，您可以配置設定以限制使用者僅上傳特定MIME型別的檔案。

## 前提条件 {#prerequisites-asset-upload-restrictions}

您必須擁有管理員許可權才能設定資產上傳限制。

## 套用資產上傳限制 {#apply-restrictions-asset-uploadsssssss}

進行設定 [!DNL Experience Manager] 若要限制使用者上傳特定MIME型別的檔案：

1. 導覽至 **[!UICONTROL 「工具>資產>資產設定」]**.

1. 按一下 **[!UICONTROL 上傳限制]**.

1. 按一下 **[!UICONTROL 新增]** 以定義允許的MIME型別。

1. 在文字方塊中指定MIME型別。 您可以按一下 **[!UICONTROL 新增]** 再次指定更多允許的MIME型別。 您也可以按一下 ![刪除圖示](assets/delete-icon.svg) 從清單中刪除任何MIME型別。

1. 单击“**[!UICONTROL 保存]**”。

**範例1：允許將所有影像和PDF檔案上傳至Experience Manager Assets**

若要允許將所有格式的影像和PDF檔案上傳至Experience Manager Assets，請執行下列設定：

![资产上传限制](assets/asset-upload-restrictions.png)

`image/*` 因為MIME型別允許上傳所有格式的影像。 `application/pdf` 因為MIME型別允許將PDF檔案上傳到Experience Manager Assets。

如果您嘗試上傳未包含在允許的MIME型別清單中的檔案，Experience Manager Assets會顯示下列錯誤訊息：

![受限制的檔案](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` 是指未包含在允許的MIME型別中的檔案名稱。

**範例2：允許將特定影像格式上傳至Experience Manager Assets**

若要將特定影像格式新增至允許的MIME型別並限制上傳所有其他資產格式，請執行下列設定：

![資產限制](assets/asset-restrictions.png)

根據影像中描述的設定，您可以將。JPG、.PNG和。GIF格式的影像上傳至Experience Manager Assets。

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
