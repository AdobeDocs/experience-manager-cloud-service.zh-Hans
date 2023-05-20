---
title: 在中管理您的PDF檔案 [!DNL Adobe Experience Manager].
description: 在中管理PDF檔案 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# 以Experience Manager Assetsas a Cloud Service管理PDF檔案 {#add-assets-to-experience-manager}

Experience Manager Assets與Document CloudPDF檢視器緊密整合，可讓您預覽PDF檔案的多個頁面。 此外，您也可以使用進階Document CloudPDF檢視器功能，例如註釋、搜尋文字、使用書籤和縮圖導覽PDF檔案，以及同一屋頂下的更多功能。 Experience Manager Assets也可讓您上傳其他支援格式的檔案，並以PDF格式預覽檔案。

Document CloudPDF檢視器可透過下列方式為AEM Assets帶來好處：
* [支援PDFDocument Cloud檢視器元件](#pdf-doc-cloud)
* [支援PDF資產的多頁預覽和註解](#multi-page)
* [支援其他格式檔案的多頁預覽](#multi-format)

> 提示
> 如果您無法取得先前上傳之PDF檔案的多頁預覽，請選取PDF並按一下 **![重新處理](/help/assets/assets/Reprocess.svg) 重新處理資產**.

## 支援PDFDocument Cloud檢視器元件 {#pdf-doc-cloud}

原生PDFDoc Cloud檢視器在AEM Assets中有下列元件：

* **使用頁面縮圖的PDF檢視器** 縮圖檢視是PDF檔案頁面的小型預覽。 使用縮圖，您可以直接跳至所需的頁面。 您可以透過存取所選PDF檔案的縮圖 ![縮圖](/help/assets/assets/thumbnail.svg) 在左窗格中。

* **使用書籤PDF檢視器** 書籤是將您導覽至檔案中內容的直接連結。 您可以透過以下方式存取所選PDF檔案的書籤： ![書籤](/help/assets/assets/bookmark.svg) 在左窗格中。

* **在PDF中搜尋** 您可以使用搜尋 ![搜尋](/help/assets/assets/Search.svg) 以查詢PDF檔案中的文字。

* **向上翻頁/向下翻頁** 使用Page Up ![向上翻頁](/help/assets/assets/ArrowUp.svg) 或Page Down ![向下翻頁](/help/assets/assets/ArrowDown.svg) 捲動檔案。

* **縮小/放大** 使用縮小顯示 ![縮小顯示](/help/assets/assets/ZoomOut.svg) 或放大顯示 ![放大顯示](/help/assets/assets/ZoomIn.svg) 來掃描檔案。

* **頁面大小** 根據熒幕大小，使用寬度或高度尺寸來配合檔案。

* **固定/取消固定PDF** 您可以使用此選項固定或取消固定原生PDF檢視器的元件。

## 支援PDF資產的多頁預覽和註解 {#multi-page}

Adobe Experience Manager資產可讓您預覽包含數個頁面的PDF檔案。 若要預覽PDF檔案的多個頁面，請考量下列步驟：

1. 請依照以下步驟操作： [在AEM中上傳資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 瀏覽您要上傳和預覽的PDF檔案。
1. 開啟檔案。
1. 預設會載入PDF檔案檢視器。 您也可以在「轉譯」面板下選取「PDF」轉譯。
1. 在「轉譯」下拉式清單中，選取 **所有轉譯**.

您也可以套用 [註解](#pdf-annotations) 在多頁預覽中切換到PDF檔案。

> 注意
> 您可以預覽的資產大小上限為100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF註解{#pdf-annotations}**

Experience Manager Assets可讓您將註解新增至PDF檔案。 一個PDF檔案可以有多個註釋。

若要為PDF檔案加上註釋，請執行下列步驟：
1. 前往Assets介面，導覽至您要加上註解的PDF檔案。 原生PDF檢視器會在右側開啟，顯示所選PDF檔案的預覽。
1. 按一下 **註釋** 從頂端功能表。
以下是可套用至PDF檔案的註解：

<table>
        <tr>
             <th> 注释 </th>
            <th> 描述 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> 注释 </td>
            <td> 選取「註解」以表示觀察。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> 文字方塊 </td>
            <td> 選取文字方塊以輸入文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 註解 </td>
            <td> 新增可以新增到PDF上特定區域的小文字或提醒。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> 文字熒光筆 </td>
            <td> 選取要以不同顏色反白的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> 文字底線 </td>
            <td> 選取要加底線的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> 刪除線 </td>
            <td> 選取要刪去的文字。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 绘图 </td>
            <td> 將視覺效果插圖插入PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 拭除工程圖 </td>
             <td> 移除或復原工程圖。 </td>
        </tr>
    </table>

## 支援其他格式檔案的多頁預覽 {#multi-format}

除了PDF檔案之外，您還可以預覽其他格式型別檔案的多個頁面。 支援的檔案格式型別為TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets會自動將這些檔案格式轉換為PDF格式，並讓它們可供預覽。

![其他格式的檔案多頁預覽](/help/assets/assets/multi-page-other-formats.png)

對於其他支援檔案格式的多頁預覽，請執行下列步驟：
1. 請依照以下步驟操作： [在AEM中上傳資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 瀏覽您要上傳和預覽的檔案。
1. 開啟檔案。
1. 在左側面板的靜態區段下選取「PDF」。 右側面板可顯示資產的多個頁面預覽。 從左側面板中選取縮圖，以選擇要預覽的頁面。

> 注意
> * 您可以預覽的資產大小上限為100 MB。
> * 要預覽的XLS或XLSX檔案大小上限為20 MB。
>


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
