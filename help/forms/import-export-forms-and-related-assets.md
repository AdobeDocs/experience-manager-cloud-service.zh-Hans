---
title: 匯入和匯出資產
seo-title: Import and export assets to [!DNL AEM Forms]
description: 您可以將Adaptive Forms和相關資產匯入和匯出至AEM執行個體。 這有助於移轉表單或跨系統移動表單。
seo-description: You can import and export Adaptive Forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 1%

---


# 匯入和匯出資產 {#importing-and-exporting-assets-to-aem-forms}

您可以在不同的之間移動表單、主題、範本、檔案片段、主題和其他資產 [!DNL AEM Forms] 執行個體。 將系統從開發或中繼伺服器移轉至生產伺服器時，需要執行這類移動。

對於透過以下方式上傳和匯入的資產： [!DNL AEM Forms] UI受到支援，建議使用Forms UI來匯出或匯入。 不建議使用AEM Package Manager匯出或匯入這類資產。

## 下載或上傳Forms &amp; Documents資產 {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] 使用者介面可讓您從AEM執行個體匯出資產，方法是將這些資產下載為AEM CRX套件或二進位檔案。 然後，您可以將下載的AEM CRX套件或二進位檔案匯入另一個AEM執行個體。

匯出和匯入方式 [!DNL AEM Forms] 除了最適化表單範本和最適化表單內容原則外，所有資產都支援使用者介面。 因此，從匯出最適化表單時 [!DNL AEM Forms] UI、相關的最適化表單範本和內容原則不會像其他相關資產一樣自動匯出。

對於這些資產型別，您必須使用AEM Package Manager在來源AEM伺服器上建立CRX套件，並在目的地伺服器上安裝套件。 如需建立及安裝套件的詳細資訊，請參閱 [部署至AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html).

### 下載Forms &amp; Documents資產 {#download-forms-amp-documents-assets}

若要下載Forms &amp; Documents資產：

1. 登入 [!DNL AEM Forms] 執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取表單資產，然後點選 **[!UICONTROL 下載]** 圖示。
1. 在「下載資產」中，選擇下列其中一個選項，然後點選 **[!UICONTROL 下載]**.

   * **下載為CRX套件：** 使用選項從以下專案下載及移動所有選取的資產及相關相依性： [!DNL AEM Forms] 執行個體到另一個。 它會將所有資產和資料夾下載為crx套件。 任何表單資產，包括在AEM (Adaptive Forms和Adaptive Form片段)、PDF檔案和資源（XSD、XFS、影像）中創作的表單，都可以透過以下套件下載 [!DNL AEM Forms] UI。
以套件形式下載資產的優點在於，它也可以下載被選取來下載的資產所使用的資產。 例如，如果您有使用表單範本、XSD和影像的最適化表單。 當您選取此最適化表單並將其下載為套件時，下載的套件也包含表單範本、XSD和影像。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。

   * **將資產下載為二進位檔案：** 使用選項僅下載表單範本(XDP)、PDF forms(PDF)、檔案(PDF)和資源（影像、結構描述、樣式表）。 您可以使用外部應用程式編輯這些資產。 它會將具有二進位檔(例如XSD、XDP、影像、PDF和XDP)的表單資產下載為.zip檔案。
您無法下載最適化Forms、最適化表單片段和主題， **[!UICONTROL 將資產下載為二進位檔案]** 選項。 若要下載這些資產，您應使用 **[!UICONTROL 下載為CRX套件]** 選項。

   選取的資產會下載為封存（.zip檔案）。

   >[!NOTE]
   >
   >AEM套件和二進位檔案都會下載為封存（.zip檔案）。 資產的範本不會隨資產一起下載。 您需要個別匯出資產範本。

### 上传资源 {#upload-forms-amp-documents-assets}

若要上傳Forms &amp; Documents資產：

1. 登入 [!DNL AEM Forms] 執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** >**檔案上傳**. 上傳表單或封裝對話方塊隨即顯示。
1. 在對話方塊中，瀏覽並選取要匯入的封裝或封存。 您也可以選取PDF檔案、XSD、影像、樣式表和XDP表單。 點選 **[!UICONTROL 開啟]**. 您選取的資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，確認上傳資產的詳細資訊，然後點選 **[!UICONTROL 上傳]**.

   如果您上傳現有表單資產，資產會隨之更新。

   >[!NOTE]
   >
   >上傳套件不會取代現有的資料夾階層。 例如，如果您在單一伺服器上的/content/dam/formsanddocuments位置有一個名為「Training」的最適化表單。 您下載最適化表單並將表單上傳到其他伺服器。 第二部伺服器也有一個名為&#39;Training&#39;的資料夾，位於相同位置/content/dam/formsanddocuments。 上傳失敗。

## 下載或上傳主題 {#downloading-or-uploading-a-theme}

替換為 [!DNL AEM Forms]，您可以建立、下載或上傳主題。 主題會像其他資產（如表單、檔案和信件）一樣建立。 您可以建立佈景主題、下載佈景主題，然後將其上傳到個別的執行個體來重複使用。 如需主題的詳細資訊，請參閱 [主題](themes.md) 在 [!DNL AEM Forms].

### 下載主題 {#downloading-a-theme}

您可以匯出主題於 [!DNL AEM Forms] 您可在其他專案或執行個體中使用的資訊。 AEM可讓您將主題下載為zip檔案，以便在執行個體上上傳。

若要下載佈景主題：

1. 登入 [!DNL AEM Forms] 執行個體。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![指南針](assets/Smock_Compass_18_N.svg) 圖示> **[!UICONTROL Forms]** > **[!UICONTROL 主題]**.
1. 選取主題並點選 **[!UICONTROL 下載]**. 主題會下載為封存（.zip檔案）。

### 上傳主題 {#uploading-a-theme}

您可以在專案上將已建立的主題與樣式預設集搭配使用。 您可以將其他人建立的主題套件上傳到您的專案中，藉此匯入這些套件。

上傳佈景主題：

1. 在Experience Manager中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL Forms主題]**.
1. 在「佈景主題」頁面中，按一下 **[!UICONTROL Forms建立]** > **[!UICONTROL Forms檔案上傳]**.
1. 在「檔案上傳」提示中，瀏覽並選取電腦上的主題套件，然後按一下 **[!UICONTROL Forms上傳]**. 主題已上傳。

<!--

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## 匯出工作流程應用程式 {#export-a-workflow-application}

您可以使用AEM封裝管理程式來匯出工作流程應用程式。 程式如下：

1. 開啟 [!DNL AEM Forms] 封裝管理員。
1. 按一下 **[!UICONTROL 建立封裝]**. 此 **[!UICONTROL 新封裝]** 對話方塊隨即顯示。
1. 指定套件的名稱、版本和群組。 单击&#x200B;**[!UICONTROL 确定]**。
1. 按一下 **[!UICONTROL 編輯]** 並開啟 **[!UICONTROL 篩選器]** 標籤。 按一下 **[!UICONTROL 新增篩選器]**. 指定工作流程應用程式的路徑。 例如，/etc/fd/dashboard/startpoints/homemortgage。 按一下 **[!UICONTROL 新增規則]**.

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。選取 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆寫]** 在ACL處理欄位中。 单击“**[!UICONTROL 保存]**”。
1. 按一下 **[!UICONTROL 建置]** 以建立封裝。

   建置套件後，您可以下載套件並將其匯入至其他伺服器。 工作流程應用程式會出現在上傳套件的伺服器上。

   >[!NOTE]
   >
   >為使工作流程應用程式正常運作，請一併匯出對應的最適化表單和工作流程模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

[!DNL AEM Forms] 使用者介面使用資料夾來排列資產。 這些資料夾用於排列在中建立的資產 [!DNL AEM Forms] 使用者介面。 您可以重新命名、建立子資料夾，以及將資產和檔案儲存在這些資料夾中。 在資料夾中組織檔案和資產可讓您將檔案群組在一起，以便輕鬆管理。 您可以選取資料夾並選擇下載或刪除。

若要建立資料夾，請完成下列步驟：

### 建立資料夾 {#create-a-folder}

1. 登入 [!DNL AEM Forms] 使用者介面位於 `https://<server>:<port>/aem/forms.html`.
1. 導覽至您要建立資料夾的位置。
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**.
1. 輸入下列詳細資料：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（必要）* 要在存放庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題中填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 在標題中輸入的任何其他特殊字元都會自動取代為連字型大小，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯。

1. 具有您定義標題的新資料夾會顯示在資產清單中的目前位置。

   如果存在具有指定名稱的資料夾，提交會失敗並出現錯誤。 您可以將滑鼠懸停在錯誤上，檢視錯誤訊息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 圖示顯示在名稱欄位旁。

   您可以點選新建立的資料夾以進入資料夾並在資料夾中建立資產或資料夾。 此外，您可以選取資料夾，並選擇將資料夾排入下載佇列、刪除資料夾或編輯資料夾名稱。

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Tap Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI allows you to search your content. Using the top bar, you can tap Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->
