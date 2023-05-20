---
title: 文件夹元数据架构
description: 瞭解如何在中建立資產資料夾的中繼資料結構 [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 10%

---

# 文件夹元数据架构 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的版面和中繼資料。

## 新增資料夾中繼資料結構表單 {#add-a-folder-metadata-schema-form}

使用資料夾中繼資料結構Forms編輯器來建立和編輯資料夾的中繼資料結構。

1. 點選/按一下 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 在「資料夾中繼資料結構Forms」頁面中，點選/按一下 **[!UICONTROL 建立]**.
1. 指定表單的名稱，然後點選/按一下 **[!UICONTROL 建立]**. 新的結構表單會列在「結構Forms」頁面中。

## 編輯資料夾中繼資料結構表單 {#edit-folder-metadata-schema-forms}

您可以編輯新新增或現有的中繼資料結構表單，其中包括：

* 选项卡
* 標籤中的表單專案。

您可以將這些表單專案對應/設定到CRX存放庫中中繼資料節點內的欄位。 您可以將新標籤或表單專案新增到中繼資料結構表單。

1. 在「結構Forms」頁面中，選取您建立的表單，然後點選/按一下 **[!UICONTROL 編輯]** 圖示加以檢視。
1. 在「資料夾中繼資料結構編輯器」頁面中，點選/按一下 **[!UICONTROL +]** 圖示以將標籤新增至表單。 若要重新命名標籤，請點選/按一下預設名稱，並在下方指定新名稱 **[!UICONTROL 設定]**.

   ![custom_tab](assets/custom_tab.png)

   若要新增更多標籤，請點選/按一下 **[!UICONTROL +]** 圖示。 點選/按一下 **[!UICONTROL X]** 刪除索引標籤。

1. 在使用中標籤中，從新增一或多個元件 **[!UICONTROL 建置表單]** 標籤。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請點選/按一下特定標籤以新增元件。

1. 若要設定元件，請選取該元件，並在下列位置修改其屬性： **[!UICONTROL 設定]** 標籤。

   如有需要，請從以下位置刪除元件： **[!UICONTROL 設定]** 標籤。

   ![configure_properties](assets/configure_properties.png)

1. 點選/按一下 **[!UICONTROL 儲存]** 以儲存變更。

### 用於建立表單的元件 {#components-to-build-forms}

此 **[!UICONTROL 建置表單]** 索引標籤會列出您在資料夾中繼資料結構表單中使用的表單專案。 此 **[!UICONTROL 設定]** 標籤會顯示您在 **[!UICONTROL 建置表單]** 標籤。 以下為中可用的表單專案清單 **[!UICONTROL 建置表單]** 標籤：

<table>
 <tbody>
  <tr>
   <td><p><strong>元件名稱</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>章节标题</p> </td>
   <td><p> 為常見元件清單新增區段標題。</p> </td>
  </tr>
  <tr>
   <td><p>单行文本</p> </td>
   <td><p> 新增單行文字屬性。 它會儲存為字串。</p> </td>
  </tr>
  <tr>
   <td><p>多值文本</p> </td>
   <td><p> 新增多值文字屬性。 它會儲存為字串陣列。</p> </td>
  </tr>
  <tr>
   <td><p>数字</p> </td>
   <td><p> 新增數字元件。</p> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p> 新增日期元件。</p> </td>
  </tr>
  <tr>
   <td><p>下拉列表</p> </td>
   <td><p> 新增下拉式清單。</p> </td>
  </tr>
  <tr>
   <td><p>标准标记</p> </td>
   <td><p> 添加标记. </p> </td>
  </tr>
  <tr>
   <td><p>隐藏字段</p> </td>
   <td><p> 新增隱藏欄位。 儲存資產時，這會傳送為POST引數。</p> </td>
  </tr>
 </tbody>
</table>

### 編輯表單專案 {#editing-form-items}

若要編輯表單專案的屬性，請點選/按一下元件，然後編輯以下屬性的全部或子集： **[!UICONTROL 設定]** 標籤。 建議只將一個欄位對應到中繼資料結構描述中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

**[!UICONTROL 欄位標籤]**：在資料夾的屬性頁面上顯示的中繼資料屬性名稱。

**[!UICONTROL 對應至屬性]**：此屬性會指定資料夾節點在CRX存放庫中儲存位置的相對路徑。 開頭是&quot;**./**&quot;，表示路徑在資料夾的節點下。

以下是屬性的有效值範例：

* `./jcr:content/metadata/dc:title`：將值儲存在資料夾的中繼資料節點，做為屬性 `dc:title`.

* `./jcr:created`：儲存資產的建立日期和時間。 這是受保護的屬性。 如果您設定這些屬性，Adobe建議您將其標籤為 [!UICONTROL 停用編輯].

為確保元件在中繼資料結構表單中正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**：用來指定JSON檔案的路徑，您可在此為選項指定索引鍵值配對。

**[!UICONTROL 預留位置]**：使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**：使用此屬性可指定清單中的選項。

**[!UICONTROL 說明]**：使用此屬性為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**：與屬性相關聯的物件類別。

## 刪除資料夾中繼資料結構表單 {#delete-folder-metadata-schema-forms}

您可以從「資料夾中繼資料結構Forms」頁面中刪除資料夾中繼資料結構表單。 若要刪除表單，請選取該表單，然後點選/按一下工具列中的「刪除」圖示。

![delete_form](assets/delete_form.png)

## 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾中繼資料結構Forms」頁面或在建立資料夾時，將資料夾中繼資料結構指派給資料夾。

如果您為資料夾設定中繼資料結構，結構表單的路徑會儲存在 `folderMetadataSchema` 下資料夾節點的屬性。*/jcr：content*.

### 從「資料夾中繼資料結構」頁面指派至結構 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 點選/按一下 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**> **[!UICONTROL 資料夾中繼資料結構]**.
1. 在「資料夾中繼資料結構Forms」頁面中，選取您要套用至資料夾的結構表單。
1. 在工具列中點選/按一下 **[!UICONTROL 套用至資料夾]**.

1. 選取要套用結構描述的資料夾，然後按一下/點選 **[!UICONTROL 套用]**. 如果資料夾上已套用中繼資料結構，則會出現警告訊息，通知您即將覆寫現有的中繼資料結構。 點選/按一下 **[!UICONTROL 覆寫]**.
1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   要查看文件夹元数据字段，请点按/单击&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 建立資料夾時指派結構 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，您可以指派資料夾中繼資料結構。 如果系統中至少存在一個資料夾中繼資料結構，則在中會顯示額外的清單 **[!UICONTROL 建立資料夾]** 對話方塊。 您可以選取所需的結構描述。 依預設，未選取任何結構描述。

1. 從 [!DNL Experience Manager Assets] 使用者介面，點選/按一下 **[!UICONTROL 建立]** （從工具列）。
1. 指定資料夾的標題和名稱。
1. 從「資料夾中繼資料結構」清單中，選取所需的結構。 然後，點選/按一下 **[!UICONTROL 建立]**.

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。
1. 要查看文件夹元数据字段，请点按/单击&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

## 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹属性。文件夹属性页面中将显示&#x200B;**[!UICONTROL 文件夹元数据]**。要查看文件夹元数据架构表单，请选择此选项卡。

在各個欄位中輸入中繼資料值，然後點選/按一下 **[!UICONTROL 儲存]** 以儲存值。 您指定的值會儲存在CRX存放庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

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
