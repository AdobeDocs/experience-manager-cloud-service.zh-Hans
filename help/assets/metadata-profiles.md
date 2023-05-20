---
title: 元数据配置文件
description: 瞭解資產的中繼資料設定檔。 瞭解如何建立中繼資料設定檔，並將其套用至資料夾資產。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 20%

---

# 元数据配置文件 {#metadata-profiles}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service | 本文 |

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料設定檔，並將其套用至資料夾。 您之後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

在Experience Manager Assets中使用設定檔的重要概念是，設定檔會指派給資料夾。 在設定檔中，設定為中繼資料設定檔的形式，以及視訊設定檔或影像設定檔。 這些設定會處理資料夾及其任何子資料夾的內容。 因此，您如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案，都會對設定檔處理這些資產的方式產生重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充分利用數位資產集合，並確保由正確的設定檔處理正確的檔案。

## 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**，然後按一下 **[!UICONTROL 建立]**.
1. 輸入中繼資料描述檔的標題，例如範例中繼資料，然後點選 **[!UICONTROL 提交]**. 此時會顯示中繼資料設定檔的編輯表單。
1. 按一下元件，然後在下列位置設定其屬性： **[!UICONTROL 設定]** 標籤。 例如，按一下 **[!UICONTROL 說明]** 元件並編輯其屬性。
編輯下列屬性 **[!UICONTROL 說明]** 元件：

   * **[!UICONTROL 欄位標籤]**  — 中繼資料屬性的顯示名稱。 它僅供使用者參考。
   * **[!UICONTROL 對應至屬性]**  — 此屬性的值會提供資產節點的相對路徑/名稱，資產節點會儲存在存放庫中。 此值應一律開頭為 `./` 因為它表示路徑在資產的節點下。

      您為指定的值 **[!UICONTROL 對應至屬性]** 會儲存為資產中繼資料節點下的屬性。 例如，如果您指定`/jcr:content/metadata/dc:desc` 作為的名稱 **[!UICONTROL 對應至屬性]**， [!DNL Adobe Experience Manager Assets] 儲存值 `dc:desc` 位於資產的中繼資料節點。

   * **[!UICONTROL 預設值]**  — 使用此屬性為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，則會將此值指派給屬性 `dc:desc` 位於資產的中繼資料節點。

      >[!NOTE]
      >
      >新增預設值至新的中繼資料屬性(不存在於 `/jcr:content/metadata` 節點)預設不會在資產的屬性頁面上顯示屬性及其值。 若要檢視上的新屬性 [!UICONTROL 屬性] 頁面，修改對應的結構描述表單。

1. （可选）从“构建表单”选项卡中向“编辑表单”添 **[!UICONTROL 加更多组件]** ，然后在“设置”选项卡中配置 **[!UICONTROL 其属性]** 。 “构建表单”选项卡中提供 **[!UICONTROL 以下属性]** :

| 组件 | 属性 |
|------------------|----------------------------------------------------|
| 章节标题 | 欄位標籤，說明 |
| 单行文本 | 欄位標籤，對應至屬性，預設值 |
| 多值文本 | 欄位標籤，對應至屬性，預設值 |
| 数字 | 欄位標籤，對應至屬性，預設值 |
| 日期 | 欄位標籤，對應至屬性，預設值 |
| 标准标记 | 欄位標籤、對應至屬性、預設值、說明 |

1. 按一下 **[!UICONTROL 完成]**. 中繼資料設定檔會新增至 **[!UICONTROL 中繼資料設定檔]** 頁面。

## 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面上，選取一個中繼資料描述檔以製作其副本。
1. 按一下 **[!UICONTROL 複製]** （從工具列）。
1. 在 **[!UICONTROL 複製中繼資料設定檔]** 對話方塊中，輸入中繼資料設定檔新復本的標題。
1. 按一下 **[!UICONTROL 複製]**. 元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

## 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面上，選取要刪除的設定檔。
1. 按一下 **[!UICONTROL 刪除中繼資料設定檔]** （在工具列中）。
1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 以確認刪除作業。 中繼資料設定檔會從清單中刪除。

## 將中繼資料設定檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

將中繼資料描述檔指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承描述檔。 將其他設定檔套用至子資料夾時，繼承會停止。 您只能將一個中繼資料設定檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的中繼資料描述檔指派給資料夾，新的描述檔會覆寫先前的描述檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至變更後新增至資料夾的資產。 您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

在使用者介面中，會以卡片名稱中出現的設定檔名稱來指出已指派給其設定檔的資料夾。

若資料夾中已有您之後已變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。 <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 將中繼資料設定檔套用至特定資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

若資料夾中已有您之後加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### 從「設定檔」使用者介面將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. 導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取您要套用至一個資料夾或多個資料夾的中繼資料設定檔。
1. 按一下 **[!UICONTROL 套用中繼資料設定檔至資料夾]** 並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 從「屬性」將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側邊欄中，按一下 **[!UICONTROL 資產]** 然後導覽至您要套用中繼資料設定檔的資料夾。
1. 在資料夾上，按一下或按一下核取記號以選取資料夾，然後按一下或按一下 **屬性**.
1. 選取 **[!UICONTROL 中繼資料設定檔]** 標籤並從下拉式選單中選取設定檔，然後按一下 **[!UICONTROL 儲存]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 全域套用中繼資料設定檔 {#applying-a-metadata-profile-globally}

除了將設定檔套用至資料夾外，您還可以全域套用設定檔，以便上傳到的任何內容都能使用 [!DNL Experience Manager Assets] 已套用選取的設定檔。

若資料夾中已有您之後已變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。 <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**若要全域套用中繼資料設定檔，請執行下列任一項作業**

* 導覽至 `https://[aem_server]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 並套用適當的設定檔，然後按一下 **[!UICONTROL 儲存]**.

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`. 新增屬性 `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. 按一下 **全部儲存**.

## 從資料夾中移除中繼資料設定檔 {#removing-a-metadata-profile-from-folders}

當您從資料夾中移除中繼資料描述檔時，任何子資料夾都會自動繼承其父資料夾中描述檔的移除動作。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以从&#x200B;**工具**&#x200B;菜单中的文件夹删除元数据配置文件，或者如果您在文件夹中，也可以直接从&#x200B;**属性**&#x200B;中删除。本节将介绍如何通过这两种方式将元数据配置文件从文件夹中删除。

### 透過設定檔使用者介面從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下Experience Manager標誌並導覽至 **[!UICONTROL 工具>資產>中繼資料設定檔]**.
1. 選取您要從資料夾或多個資料夾中移除的中繼資料描述檔。
1. 按一下 **[!UICONTROL 從資料夾中移除中繼資料設定檔]** 並選取您要用來從中移除設定檔的資料夾或多個資料夾，然後按一下 **[!UICONTROL 完成]**.

   您可以確認中繼資料描述檔不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下Experience Manager標誌並導覽 **[!UICONTROL 資產]** 然後移至您要從中移除中繼資料設定檔的資料夾。
1. 在資料夾上，按一下核取記號以選取資料夾，然後按一下 **[!UICONTROL 屬性]**.
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

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
