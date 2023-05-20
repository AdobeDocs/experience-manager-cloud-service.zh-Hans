---
title: 层叠元数据
description: 本文說明如何定義資產的階層式中繼資料。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 1d3ad496-a964-476e-b1da-4aa6d8ad53b7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 15%

---

# 階層式中繼資料 {#cascading-metadata}

擷取資產的中繼資料資訊時，使用者會在各種可用欄位中提供資訊。 您可以根據在其他欄位中選取的選項，顯示特定的中繼資料欄位或欄位值。 這類條件式顯示中繼資料稱為階層式中繼資料。 換言之，您可以在特定中繼資料欄位/值與一或多個欄位和/或其值之間建立相依性。

使用中繼資料結構描述來定義顯示階層式中繼資料的規則。 例如，如果您的中繼資料結構描述包含資產型別欄位，您可以根據使用者選取的資產型別，定義要顯示的相關欄位集。

以下是您可以定義階層式中繼資料的一些使用案例：

* 在需要使用者位置的地方，根據使用者選擇的國家和州顯示相關的城市名稱。
* 根據使用者選擇的產品類別，在清單中載入相關的品牌名稱。
* 根據在另一個欄位中指定的值切換特定欄位的可見度。 例如，如果使用者想要在不同地址交付出貨，則顯示個別的出貨位址列位。
* 根據其他欄位中指定的值，將欄位指定為必填欄位。
* 根據在另一個欄位中指定的值，變更針對特定欄位顯示的選項。
* 根據在另一個欄位中指定的值，在特定欄位中設定預設中繼資料值。

## 在中設定階層式中繼資料 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

假設您要根據選取的資產型別顯示階層式中繼資料。 部分範例

* 對於視訊，顯示適用的欄位，例如格式、轉碼器、持續時間等。
* 對於Word或PDF檔案，顯示欄位，例如頁數、作者等。

無論選擇的資產型別為何，都會將版權資訊顯示為必填欄位。

1. 點選/按一下 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 在&#x200B;**[!UICONTROL 架构表单]**&#x200B;页面中，选择一个架构表单，然后点按/单击工具栏中的&#x200B;**[!UICONTROL 编辑]**，以编辑架构。

   ![select_form](assets/select_form.png)

1. （選用）在中繼資料結構編輯器中，建立新欄位以進行條件化。 在中指定名稱和屬性路徑 **[!UICONTROL 設定]** 標籤。

   若要建立新標籤，請點選/按一下 `+` 以新增索引標籤，然後新增中繼資料欄位。

   ![add_tab](assets/add_tab.png)

1. 新增資產型別的下拉式清單欄位。 在中指定名稱和屬性路徑 **[!UICONTROL 設定]** 標籤。 新增選擇性說明。

   ![asset_type_field](assets/asset_type_field.png)

1. 機碼值組是提供給表單使用者的選項。 您可以手動或從JSON檔案提供索引鍵值配對。

   * 若要手動指定值，請選取 **[!UICONTROL 手動新增]**，然後點選/按一下 **[!UICONTROL 新增選擇]** 和指定選項文字和值。 例如，指定視訊、PDF、Word和影像資產型別。

   * 若要動態擷取JSON檔案中的值，請選取 **[!UICONTROL 透過JSON路徑新增]** 和提供JSON檔案的路徑。 [!DNL Experience Manager] 向使用者呈現表單時，會即時擷取機碼值組。

   兩個選項互斥。 您無法從JSON檔案匯入選項並手動編輯。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >新增JSON檔案時，索引鍵/值組不會顯示在中繼資料結構編輯器中，但可在發佈的表單中使用。

   >[!NOTE]
   >
   >新增選項時，如果按一下彈出式欄位，介面會扭曲，且選項的刪除圖示會停止運作。 在儲存變更之前，請勿按下拉式清單。 如果您遇到此問題，請儲存結構描述並再次開啟以繼續編輯。

1. （選用）新增其他必要欄位。 例如，資產型別視訊的格式、轉碼器和持續時間。

   同樣地，為其他資產型別新增相依欄位。 例如，為檔案資產(例如PDF和Word檔案)新增欄位頁數與作者。

   ![video_dependent_field](assets/video_dependent_fields.png)

1. 若要在資產型別欄位與其他欄位之間建立相依性，請選擇相依性欄位，然後開啟 **[!UICONTROL 規則]** 標籤。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 下 **[!UICONTROL 需求]**，選擇 **[!UICONTROL 必要，根據新規則]** 選項。
1. 点按／单 **[!UICONTROL 击添加规则]** ，然后选择“资 **[!UICONTROL 产类型]** ”字段以创建依赖关系。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 点按／单击 **[!UICONTROL 完成]** ，以保存更改。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >具有手動預先定義值的下拉式清單可與規則搭配使用。 具有已設定JSON路徑的下拉式功能表，無法與使用預先定義值來套用條件的規則搭配使用。 如果在執行階段從JSON載入值，則無法套用預先定義的規則。

1. 在“可 **[!UICONTROL 见性]**”下，根据新 **[!UICONTROL 规则选项选择“可见]** ”。

1. 点按／单 **[!UICONTROL 击添加规则]** ，然后选择“资 **[!UICONTROL 产类型]** ”字段以创建依赖关系。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 点按／单击 **[!UICONTROL 完成]** ，以保存更改。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!CAUTION]
   >
   >若要重設值，請按一下或點選空白字元或介面上值以外的任何位置。 如果值已重設，請再次選取值。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

1. 同樣地，在「資產型別」欄位中的「視訊」值與其他欄位（例如「轉碼器」和「持續時間」）之間建立相依性。
1. 重複步驟以建立檔案資產(PDF和Word)之間的相依性。 [!UICONTROL 資產型別] 欄位和欄位，例如 [!UICONTROL 頁數] 和 [!UICONTROL 作者].
1. 单击“**[!UICONTROL 保存]**”。將中繼資料結構描述套用至資料夾。

1. 導覽至您套用中繼資料結構的資料夾，然後開啟資產的屬性頁面。 視您在「資產型別」欄位中的選擇而定，會顯示相關的階層式中繼資料欄位。

   ![視訊資產的階層式中繼資料](assets/video_asset.png)
   *圖：視訊資產的階層式中繼資料*

   ![檔案資產的階層式中繼資料](assets/doc_type_fields.png)
   *圖：檔案資產的階層式中繼資料*

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
