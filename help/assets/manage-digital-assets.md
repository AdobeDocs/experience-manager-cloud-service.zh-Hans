---
title: 管理数字资源
description: 瞭解各種資產管理和編輯方法
contentOwner: AG
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '4378'
ht-degree: 11%

---

# 管理资源 {#manage-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

本文說明如何在中管理和編輯資產 [!DNL Adobe Experience Manager Assets]. 管理 [!DNL Content Fragments]，請參閱 [[!DNL Content Fragments]](content-fragments/content-fragments.md) 資產。

## 创建文件夹 {#creating-folders}

例如，組織資產集合時，所有 `Nature` 您可以建立資料夾來將它們放在一起。 您可以使用資料夾來分類及組織您的資產。 [!DNL Experience Manager Assets] 您不需要在資料夾中組織資產才能更佳運作。

>[!NOTE]
>
>* 共用型別的資產資料夾 `sling:OrderedFolder`，在共用至Experience Cloud時不受支援。 如果要共用資料夾，請勿選取 [!UICONTROL 已訂購] 建立資料夾時。
>* Experience Manager不允許使用 `subassets` word做為資料夾的名稱。 這是為包含複合資產之子資產的節點保留的關鍵字


1. 導覽至數位資產資料夾中您要建立新資料夾的位置。 在功能表中，按一下 **[!UICONTROL 建立]**. 選取 **[!UICONTROL 新增資料夾]**.
1. 在 **[!UICONTROL 標題]** 欄位中，提供資料夾名稱。 根據預設，DAM會使用您提供的標題作為資料夾名稱。 建立資料夾後，您可以覆寫預設值並指定另一個資料夾名稱。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的資料夾會顯示在數位資產資料夾中。

不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不能包含下列任一字元： `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不能包含下列任一字元： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 上传资源 {#uploading-assets}

另請參閱 [將數位資產新增至Experience Manager](add-assets.md).

## 偵測重複資產 {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

如果DAM使用者上傳一個或多個已存在於存放庫中的資產， [!DNL Experience Manager] 會偵測重複並通知使用者。 重複資料偵測預設為停用，因為它可能會對效能造成影響，具體取決於存放庫的大小和上傳的資產數量。

若要啟用此功能：

1. 導覽至 **[!UICONTROL 「工具>資產>資產設定」]**.

1. 按一下 **[!UICONTROL 資產重複偵測器]**.

1. 於 [!UICONTROL 資產重複偵測器頁面]，按一下 **[!UICONTROL 已啟用]**.

   `dam:sha1` 「偵測中繼資料」欄位的值可確保即使檔案名稱不同，仍會偵測到重複的資產。

1. 单击“**[!UICONTROL 保存]**”。

   ![资源重复检测器](assets/asset-duplication-detector.png)

>[!NOTE]
>
>如果您已使用設定重複偵測器 `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` 設定檔案（OSGi設定），您可以繼續使用，但Adobe建議使用新方法。


啟用後，Experience Manager會將重複資產的通知傳送到Experience Manager收件匣。 此為多個重複專案的彙總結果。 使用者可以選擇根據結果移除資產。

![重複資產的收件匣通知](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>當您將資產上傳到存放庫時，Experience Manager會偵測到重複並通知您前100個重複資產。

## 预览资源 {#previewing-assets}

若要預覽資產，請依照下列步驟操作。

1. 從Assets使用者介面，導覽至您要預覽的資產位置。
1. 點選所需的資產以將其開啟。

1. 在預覽模式中，縮放選項可用於 [支援的影像型別](/help/assets/file-format-support.md) （使用互動式編輯）。

   若要放大資產，請點選/按一下 `+` （或點選/按一下資產上的放大鏡）。 若要縮小顯示，請點選/按一下 `-`. 放大時，您可以透過平移仔細檢視影像的任何區域。 重設縮放箭頭會將您帶回原始檢視。

   點選 **[!UICONTROL 重設]** 將檢視重設為原始大小。

## 编辑属性 {#editing-properties}

1. 導覽至您要編輯其中繼資料的資產位置。

1. 選取資產，然後點選/按一下 **[!UICONTROL 屬性]** 以檢視資產屬性。 或者，選擇 **[!UICONTROL 屬性]** 資產卡上的快速動作。

   ![properties_quickaction](assets/properties_quickaction.png)

1. 在 [!UICONTROL 屬性] 頁面，編輯各種標籤下的中繼資料屬性。 例如，在 **[!UICONTROL 基本]** 標籤、編輯標題、說明等。

   >[!NOTE]
   >
   >「 」的版面 [!UICONTROL 屬性] 頁面和可用的中繼資料屬性取決於基礎中繼資料結構。 若要瞭解如何修改 [!UICONTROL 屬性] 頁面，請參閱 [中繼資料結構](/help/assets/metadata-schemas.md).

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 若要在特定期間後停用資產，請從日期選擇器旁的停用日期/時間 **[!UICONTROL 關閉時間]** 欄位。 停用日期應晚於資產的啟用日期。 晚於 [!UICONTROL 關閉時間]，無法透過Assets網頁介面或HTTP API使用資產及其轉譯。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在 **[!UICONTROL 標籤]** 欄位中，選取一或多個標籤。 若要新增自訂標籤，請在方塊中輸入標簽名稱，然後選取 `Enter` 金鑰。 新標籤儲存在中 [!DNL Experience Manager].

   YouTube需要標籤才能發佈，而且必須具備YouTube連結（如果可以找到合適的連結）。

   >[!NOTE]
   >
   >若要建立標籤，您必須擁有寫入許可權： `/content/cq:tags/default` CRX存放庫中的路徑。

1. 點選/按一下 **[!UICONTROL 儲存並關閉]**.

1. 導覽至「資產」使用者介面。 編輯的中繼資料屬性（包括標題、說明和標籤）會顯示在「卡片」檢視的資產卡片上，以及「清單」檢視的相關欄下。

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## 复制资产 {#copying-assets}

當您複製資產或資料夾時，將會複製整個資產或資料夾及其內容結構。 複製的資產或資料夾會複製到目標位置。 來源位置的資產不會變更。

資產特定副本的少數屬性不會結轉。 部分範例包括：

* 資產ID、建立日期和時間，以及版本和版本記錄。 其中一些屬性由屬性指示 `jcr:uuid`， `jcr:created`、和 `cq:name`.

* 每個資產及其每個轉譯的建立時間和參照路徑都是唯一的。

其他屬性和中繼資料資訊會保留。 複製資產時不會建立部分副本。

1. 從「資產」UI中，選取一或多個資產，然後點選/按一下 **[!UICONTROL 複製]** 圖示加以檢視。 或者，選取 **[!UICONTROL 複製]** ![copy_icon](assets/copy_icon.png) 從資產卡片快速動作。

   >[!NOTE]
   >
   >如果您使用 [!UICONTROL 複製] 快速動作，您一次只能複製一個資產。

1. 導覽至您要複製資產的位置。

   >[!NOTE]
   >
   >如果您在相同位置複製資產， [!DNL Experience Manager] 會自動產生名稱的變數。 例如，如果您複製標題為 `Square`， [!DNL Experience Manager] 自動為其副本產生標題 `Square1`.

1. 按一下 **[!UICONTROL 貼上]** 工具列中的資產圖示。 資產會複製到此位置。

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >此 **[!UICONTROL 貼上]** 圖示會一直顯示在工具列中，直到完成貼上作業為止。

### 移動或重新命名資產 {#moving-or-renaming-assets}

1. 導覽至您要移動的資產位置。

1. 選取資產，然後點選/按一下 **[!UICONTROL 移動]** 圖示 ![move_icon](assets/move_icon.png) （從工具列）。

1. 在「移動資產」精靈中，執行下列任一項作業：

   * 指定資產移動後的名稱。 然後點選/按一下 **[!UICONTROL 下一個]** 以繼續進行。

   * 點選/按一下 **[!UICONTROL 取消]** 以停止程式。
   >[!NOTE]
   >
   >* 如果新位置沒有同名的資產，您可以為該資產指定相同的名稱。 不過，如果您將資產移至有相同名稱的資產存在的位置，則應使用不同的名稱。 如果您使用相同的名稱，系統會自動產生名稱的變數。 例如，如果資產的名稱為Square，則系統會為其副本產生名稱Square1。
   >* 重新命名時，檔案名稱中不允許有空格。


1. 於 **[!UICONTROL 選取目的地]** 對話方塊，請執行下列任一項作業：

   * 導覽至資產的新位置，然後點選/按一下 **[!UICONTROL 下一個]** 以繼續進行。

   * 點選/按一下 **[!UICONTROL 返回]** 以返回 **[!UICONTROL 重新命名]** 畫面。

1. 如果要移動的資產有任何參考頁面、資產或集合，則 **[!UICONTROL 調整引用]** 標籤會出現在 **[!UICONTROL 選取目的地]** 標籤。

   請執行以下任一項作業： **[!UICONTROL 調整引用]** 畫面：

   * 根據新的詳細資料指定要調整的參照，然後點選/按一下 **[!UICONTROL 移動]** 以繼續進行。

   * 從 **[!UICONTROL 調整]** 欄中，選取/取消選取資產的參照。
   * 點選/按一下 **[!UICONTROL 返回]** 以返回 **[!UICONTROL 選取目的地]** 畫面。

   * 點選/按一下 **[!UICONTROL 取消]** 以停止移動作業。

   如果您不更新引用，引用會繼續指向資產的上一個路徑。 如果您調整參照，參照會更新為新的資產路徑。

### 管理轉譯 {#managing-renditions}

1. 您可以新增或移除資產的轉譯，但原始資產除外。 導覽至您要新增或移除轉譯的資產位置。

1. 點選/按一下資產以開啟其資產頁面。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 點選/按一下「全域導覽」圖示，然後選取 **[!UICONTROL 轉譯]** 從清單中。

   ![renditions_menu](assets/renditions_menu.png)

1. 在 **[!UICONTROL 轉譯]** 面板，檢視針對資產產生的轉譯清單。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >依預設， [!DNL Experience Manager Assets] 不會在預覽模式下顯示資產的原始轉譯。 如果您是管理員，則可以使用覆蓋圖來設定 [!DNL Assets] 在預覽模式下顯示原始轉譯。

1. 選取轉譯以檢視或刪除轉譯。

   **刪除轉譯**

   從中選擇轉譯 **[!UICONTROL 轉譯]** 面板，然後點選/按一下 **[!UICONTROL 刪除轉譯]** 圖示加以檢視。 資產處理完成後，無法大量刪除轉譯。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以進行自訂 [!DNL Experience Manager] 以刪除特定轉譯或刪除資產，並重新上傳已刪除的資產。

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **上傳新轉譯**

   导航到资源的资源详细信息页面，然后点击/单击工具栏中的&#x200B;**[!UICONTROL “添加演绎版”]**&#x200B;图标以上传资源的新演绎版。

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >如果从&#x200B;**[!UICONTROL “演绎版”]**&#x200B;面板选择演绎版，则工具栏更改上下文并仅显示与该演绎版相关的那些操作。不显示“上传演绎版”图标等选项。 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以設定要在影像或視訊資產的詳細資訊頁面中顯示的轉譯尺寸。 根據您指定的維度，「資產」會顯示具有精確或最接近維度的轉譯。

   要在资源详细信息级别配置图像的演绎版尺寸，请叠加 `renditionpicker` 节点 (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) 并配置宽度属性的值。配置属性&#x200B;**[!UICONTROL 大小（长）(以 KB 计）]**&#x200B;代替宽度，以根据图像大小在资源详细信息页面上自定义演绎版。对于基于大小的自定义，如果匹配的演绎版的大小大于原始演绎版，则属性 `preferOriginal` 将首选项分配给原始演绎版。

   同樣地，您可以透過覆蓋來自訂註釋頁面影像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   若要設定視訊資產的轉譯維度，請導覽至 `videopicker` CRX存放庫中位於位置的節點 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`，覆蓋節點，然後編輯適當的屬性。

   >[!NOTE]
   >
   >視訊註解僅支援使用HTML5相容視訊格式的瀏覽器。 此外，視瀏覽器而定，支援不同的視訊格式。 不過，視訊註解尚不支援MXF視訊格式。

## 刪除資產 {#delete-assets}

若要從其他頁面解析或移除傳入參照，請先更新相關參照，然後再刪除資產。

此外，使用覆蓋圖停用強制刪除按鈕，以禁止使用者刪除參照的資產並留下中斷的連結。

1. 導覽至您要刪除的資產位置。

1. 選取資產，然後按一下 **[!UICONTROL 刪除]** ![delete_icon](assets/do-not-localize/delete-icon.png) （從工具列）。

1. 在確認對話方塊中，按一下：

   * **[!UICONTROL 取消]** 停止動作
   * **[!UICONTROL 刪除]** 若要確認動作：

      * 如果資產沒有參考資料，則會刪除資產。
      * 如果資產有參考資料，則會出現錯誤訊息，通知您 **[!UICONTROL 一個或多個資產被引用]**. 您可以選取 **[!UICONTROL 強制刪除]** 或 **[!UICONTROL 取消]**.

   >[!NOTE]
   >
   >您需要dam/asset的刪除許可權才能刪除資產。 如果您只有修改許可權，則只能編輯資產中繼資料並將註解新增至資產。 不過，您無法刪除資產或其中繼資料。

   >[!NOTE]
   >
   >若要從其他頁面解析或移除傳入參照，請先更新相關參照，然後再刪除資產。 您可以禁止刪除參照的資產，因為這會造成連結損毀。 使用覆蓋圖停用強制刪除按鈕。

## 下载资源 {#download-assets}

另請參閱 [資產下載來源 [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## 發佈或取消發佈資產 {#publish-assets}

1. 導覽至您要發佈或要從發佈環境移除（取消發佈）的資產或資產資料夾位置。

1. 選取要發佈或取消發佈的資產或資料夾，然後選取 **[!UICONTROL 管理發布]** ![管理出版物選項](assets/do-not-localize/globe-publication.png) 工具列中的選項。 或者，若要快速發佈，請選取 **[!UICONTROL 快速發佈]** 工具列中的選項。 如果您要發佈的資料夾包含空白資料夾，則不會發佈空白資料夾。

1. 選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 選項。

   ![取消發佈動作](assets/unpublish_action.png)
   *圖：發佈和取消發佈選項以及排程選項。*

1. 選取 **[!UICONTROL 現在]** 以立即對資產採取行動，或選取 **[!UICONTROL 稍後]** 以排程動作。 如果您選擇 **[!UICONTROL 稍後]** 選項。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 發佈時，如果資產參考其他資產，其參考會列在精靈中。 只會顯示自上次發佈後未發佈或修改的參考。 選擇要發佈的參照。

1. 取消發佈時，如果資產參考其他資產，請選擇您要取消發佈的參考。 单击&#x200B;**[!UICONTROL 取消发布]**。在確認對話方塊中，按一下 **[!UICONTROL 取消]** 以停止動作，或按一下 **[!UICONTROL 取消發佈]** 以確認資產會在指定的日期取消發佈。

瞭解以下與發佈或取消發佈資產或資料夾相關的限制和提示：

* 的選項 [!UICONTROL 管理發布] 僅適用於具有復寫許可權的使用者帳戶。
* 取消發佈複雜資產時，請僅取消發佈資產。 請避免取消發佈引用，因為這些引用可能會被其他已發佈的資產引用。
* 未發佈空白資料夾。
* 如果您發佈正在處理的資產，只會發佈原始內容。 缺少轉譯。 請等待處理完成，然後在處理完成時發佈或重新發佈資產。

## 已關閉的使用者群組 {#closed-user-group}

封閉式使用者群組(CUG)可用來限制存取從發佈的特定資產資料夾 [!DNL Experience Manager]. 如果您為資料夾建立CUG，則資料夾（包括資料夾資產和子資料夾）的存取權僅限於指派的成員或群組。 若要存取資料夾，使用者必須使用其安全性認證登入。

CUG是限制資產存取權的額外方式。 您也可以為資料夾設定登入頁面。

1. 從「資產」UI中選取資料夾，然後點選/按一下工具列中的「屬性」圖示以顯示屬性頁面。
1. 從 **[!UICONTROL 許可權]** 標籤，新增成員或群組 **[!UICONTROL 已關閉的使用者群組]**.

   ![add_user](assets/add_user.png)

1. 若要在使用者存取資料夾時顯示登入畫面，請選取 **[!UICONTROL 啟用]** 選項。 然後，選取登入頁面的路徑 [!DNL Experience Manager]，並儲存變更。

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >如果您未指定登入頁面的路徑， [!DNL Experience Manager] 會在發佈執行個體中顯示預設登入頁面。

1. 發佈資料夾，然後嘗試從發佈執行個體存取它。 登入畫面隨即顯示。
1. 如果您是CUG成員，請輸入您的安全性認證。 資料夾顯示於 [!DNL Experience Manager] 驗證您的身分。

## 搜索资源 {#search-assets}

搜尋資產是使用數位資產管理系統的核心，無論是供創意人員進一步使用、供業務使用者和行銷人員健全管理資產，還是DAM管理員管理。

如需簡單、進階和自訂搜尋以探索和使用最適當的資產，請參閱 [搜尋中的資產 [!DNL Experience Manager]](/help/assets/search-assets.md).

## 快速操作 {#quick-actions}

快速動作圖示一次只適用於單一資產。 視您的裝置而定，執行下列動作以顯示快速動作圖示：

* 觸控裝置：觸控並按住。 例如，在iPad上，您可以點選並按住資產，以便顯示快速動作。
* 非觸控裝置：游標暫留。 例如，在案頭裝置上，如果您將指標停留在資產縮圖上，則會顯示快速動作列。

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then click/tap the **[!UICONTROL Edit]** icon in the toolbar.
    * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, tap/click the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Tap/click the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Tap/click the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## 时间线 {#timeline}

時間軸可讓您檢視所選專案的各種事件，例如資產的使用中工作流程、註解/註解、活動記錄及版本。

![排序資產的時間軸專案](assets/sort_timeline.gif)
*圖：排序資產的時間軸專案*

>[!NOTE]
>
>在 [集合主控台](/help/assets/manage-collections.md#navigate-the-collections-console)，則 **[!UICONTROL 全部顯示]** list提供僅檢視註解和工作流程的選項。 此外，時間軸只會顯示在主控台中列出的頂層集合。 如果您在任何集合內導覽，則不會顯示它。

>[!NOTE]
>
>時間軸包含數個 [內容片段專屬選項](content-fragments/content-fragments.md).

## 為資產加上註釋 {#annotating}

註解是新增至影像或影片的評論或說明附註。 註解讓行銷人員能夠共同作業並留下有關資產的意見回饋。

只有具備HTML5相容視訊格式的瀏覽器才支援視訊註解。 Assets支援的視訊格式取決於瀏覽器。 不過，視訊註解尚不支援MXF視訊格式。

>[!NOTE]
>
>對於內容片段， [註解會在片段編輯器中建立](content-fragments/content-fragments.md).

1. 導覽至您要新增註解的資產位置。
1. 點選/按一下 **[!UICONTROL 註釋]** 圖示來自下列其中一項：

   * [快速操作](#quick-actions)
   * 在選取資產或導覽至資產頁面後，從工具列移除

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>對於非管理員使用者，只有在使用者擁有下列專案的讀取許可權時，才會顯示建議： `/home` 在CRXDE中。

![chlimage_1-235](assets/chlimage_1-235.png)

1. 新增註釋後，按一下 **[!UICONTROL 新增]** 以儲存。 註解的通知會傳送給Aaron。

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >儲存註解之前，您可以新增多個註解。

1. 點選/按一下 **[!UICONTROL 關閉]** 退出「註釋」模式。
1. 若要檢視通知，請使用Aaron MacDonald的憑證登入Assets，然後按一下 **[!UICONTROL 通知]** 圖示以檢視通知。

   >[!NOTE]
   >
   >註解也可以新增到視訊資產。 在註解視訊時，播放器會暫停，讓您在影格上註解。 如需詳細資訊，請參閱 [管理視訊資產](manage-video-assets.md). 不過，視訊註解尚不支援MXF視訊格式。

1. 若要選擇不同顏色以便區分使用者，請按一下/點選「設定檔」圖示，然後按一下/點選 **[!UICONTROL 我的偏好設定]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   在&#x200B;**[!UICONTROL 批注颜色]**&#x200B;框中指定所需颜色，然后单击/点按&#x200B;**[!UICONTROL 接受]**。

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>您也可以將註解新增至集合。 不過，如果集合包含子集合，您只能將註解/註解新增至父集合。 「註釋」選項不適用於子集合。

### 檢視儲存的註解 {#viewing-saved-annotations}

您一次只能檢視一個註解。

>[!NOTE]
>
>如果您選取多個註解，最新的註解將顯示在使用者介面上。
>
>僅支援將註解資產列印為PDF的多重選取。

1. 若要檢視資產的已儲存附註，請導覽至資產位置，然後開啟資產的資產頁面。

1. 點選/按一下「全域導覽」圖示，然後選擇 **[!UICONTROL 時間表]** 從清單中。

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. 从时间线的&#x200B;**[!UICONTROL 显示全部]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 注释]**&#x200B;以根据注释过滤结果。

   ![chlimage_1-240](assets/chlimage_1-240.png)

   點選/按一下中的註解 **[!UICONTROL 時間表]** 面板來檢視影像上的對應註解。

   ![chlimage_1-241](assets/chlimage_1-241.png)

   點選/按一下 **[!UICONTROL 刪除]**，以刪除特定註解。

### 列印註解 {#printing-annotations}

如果資產有註解或受到稽核工作流程的約束，您可以列印資產以及註解和稽核狀態，作為PDF檔案供離線稽核。

您也可以選擇只列印註解或檢閱狀態。

>[!NOTE]
>
>將已附註的資產列印為PDF時，您可以選取多個附註。

若要列印註釋和檢閱狀態，請點選/按一下 **[!UICONTROL 列印]** 圖示並依照精靈中的指示操作。 此 **[!UICONTROL 列印]** 圖示只有在資產至少有一個指派給它的註解或稽核狀態時才會出現在工具列中。

1. 從Assets UI開啟資產的預覽頁面。
1. 执行下列操作之一：

   * 若要列印所有附註和稽核狀態，請略過步驟3並直接跳至步驟4。
   * 若要列印特定註解及檢閱狀態，請開啟 [時間表](/help/assets/manage-digital-assets.md#timeline) 然後前往步驟3。

1. 若要列印特定註解，請從時間軸中選取註解。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   若要僅列印稽核狀態，請從時間軸中選取它。

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. 點選/按一下 **[!UICONTROL 列印]** 圖示加以檢視。

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. 從「列印」對話方塊中，選擇您希望註釋/審閱狀態顯示在PDF上的位置。 例如，如果您希望註解/狀態列印在包含已列印影像的頁面的右上角，請使用 **左上方** 設定。 預設會選取它。

   ![chlimage_1-245](assets/chlimage_1-245.png)

   您可以根据希望在打印的 PDF 中显示批注/状态的位置选择其他设置。如果希望批注/状态显示在与打印资产不同的页面中，请选择&#x200B;**[!UICONTROL 下一页]**。

1. 按一下 **[!UICONTROL 列印]**. 根据您在步骤 2 中选择的选项，生成的 PDF 会在指定位置显示批注/状态。例如，如果您选择使用&#x200B;**左上角**&#x200B;设置打印批注和审阅状态，则生成的输出将类似于此处描述的 PDF 文件。

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. 使用右上方的選項下載或列印PDF。

   ![chlimage_1-247](assets/chlimage_1-247.png)

   若要修改演算PDF檔案的外觀，例如註解與狀態的字型顏色、大小與樣式、背景顏色，請開啟 **[!UICONTROL 註解PDF設定]** 從Configuration Manager中，修改所需的選項。 例如，若要變更已核准狀態的顯示顏色，請修改對應欄位中的顏色代碼。 如需有關變更註解字型顏色的資訊，請參閱 [註釋](/help/assets/manage-digital-assets.md#annotating).

   返迴轉譯的PDF檔案並重新整理。 重新整理的PDF會反映您所做的變更。

## 资源版本控制 {#asset-versioning}

版本設定功能會在特定時間點建立數位資產的快照。 版本設定功能有助於將資產在稍後還原成先前的狀態。 例如，如果您要復原對資產所做的變更，請還原該資產的未編輯版本。

以下是建立版本的情況：

* 您可以修改不同應用程式中的影像，然後上傳至Assets。 會建立影像的版本，這樣就不會覆寫原始影像。
* 您可以編輯資產的中繼資料。
* 您使用 [!DNL Experience Manager] 案頭應用程式，以簽出現有資產並儲存您的變更。 每次儲存資產時都會建立新版本。

您也可以透過工作流程啟用自動版本設定。 當您建立資產的版本時，中繼資料和轉譯會與版本一起儲存。 轉譯會取代相同的影像，例如上傳之JPEG檔案的PNG轉譯。

版本設定功能可讓您執行下列動作：

* 建立資產的版本。
* 檢視資產的目前修訂版本。
* 將資產還原至舊版。

1. 導覽至您要建立版本的資產位置，然後點選/按一下以開啟其資產頁面。

1. 點選/按一下「全域導覽」圖示，然後選擇 **[!UICONTROL 時間表]** 功能表中的。

   ![时间线](assets/timeline.png)

1. 點選/按一下 **[!UICONTROL 動作]** （箭頭）圖示來檢視您可以對資產執行的可用動作。

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. 點選/按一下 **[!UICONTROL 另存為版本]** 以建立資產的版本。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 新增標籤和註解，然後按一下 **[!UICONTROL 建立]** 以建立版本。 或者，點選/按一下 **取消** 以結束作業。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 要查看新版本，请从资产详细信 **[!UICONTROL 息页面或资产UI中打开时间轴中的显示全部]** ，然后选择版 **[!UICONTROL 本]**。 为资产创建的所有版本都列在时间轴选项卡下。 您可以通过单击下拉箭头并从列表中选择版本，来过滤列 **[!UICONTROL 表以显示]** “版本”。

   ![versions_option](assets/versions_option.png)

1. 選取資產的特定版本以預覽資產，或讓資產出現在Assets UI中。

   ![select_version](assets/select_version.png)

1. 為版本新增標籤和註解，以還原到Assets UI中的特定版本。

   ![save_version](assets/save_version.png)

1. 要为版本生成预览，请点按/单击&#x200B;**[!UICONTROL 预览版本]**。
1. 若要在資產UI中顯示此版本，請選取「 」 **[!UICONTROL 還原為此版本]**.
1. 若要比較兩個版本，請前往資產的資產頁面，然後點選/按一下要與目前版本比較的版本。

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. 從時間軸中，選取您要比較的版本，並將滑桿拖曳至左側，以將此版本重疊在目前版本上並進行比較。

   ![compare_versions](assets/compare_versions.png)

### 在資產上開始工作流程 {#starting-a-workflow-on-an-asset}

1. 導覽至您要開始工作流程的資產位置，然後點選/按一下資產以開啟資產頁面。
1. 點選/按一下「全域導覽」圖示，然後選擇 **[!UICONTROL 時間表]** 從功能表顯示時間軸。

   ![時間軸–1](assets/timeline-1.png)

1. 點選/按一下 **[!UICONTROL 動作]** （箭頭）圖示來開啟資產可用的動作清單。

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. 點選/按一下 **[!UICONTROL 開始工作流程]** 從清單中。

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. 在 **[!UICONTROL 開始工作流程]** 對話方塊中，從清單中選取工作流程模型。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. （選用）指定工作流程的標題，可用來參考工作流程例項。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 点按／单击 **[!UICONTROL 开始]** ，然后点按／单 **[!UICONTROL 击对话框中的继]** 续，以进行确认。 工作流的每个步骤都会作为事件显示在时间轴中。

   ![chlimage_1-256](assets/chlimage_1-256.png)

## 收藏集 {#collections}

集合是一組經過排序的資產。 使用收藏集可在用户之间共享资源。

* 集合可以包含來自不同位置的資產，因為它們僅包含對這些資產的引用。 每個集合都會維護資產的參考完整性。
* 您可以與具有不同許可權層級的多個使用者共用集合，包括編輯、檢視等。

若要瞭解集合管理的詳細資訊，請參閱 [管理集合](/help/assets/manage-collections.md).

## 在案頭應用程式中檢視資產或AdobeAsset Link時隱藏過期的資產 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] 案頭應用程式可讓您從Windows或Mac案頭存取DAM存放庫。 AdobeAsset Link允許從受支援記憶體取資產 [!DNL Creative Cloud] 案頭應用程式。

從內瀏覽資產時 [!DNL Experience Manager] 使用者介面中，不會顯示過期的資產。 若要防止在從案頭應用程式和Asset Link瀏覽資產時檢視、搜尋和擷取已到期資產，管理員可以執行下列設定。 此設定適用於所有使用者，無論管理員許可權為何。

執行下列CURL命令。 確定讀取存取權於 `/conf/global/settings/dam/acpapi/` 適用於存取資產的使用者。 屬於的使用者 `dam-user` 預設為群組擁有許可權。

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

若要瞭解更多，請參閱如何 [使用案頭應用程式瀏覽DAM資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 和 [如何使用Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).

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
