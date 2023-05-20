---
title: 管理數位資產集合
description: 瞭解Adobe Experience Manager資產中的集合概念。 瞭解如何與其他使用者一起收集、管理、編輯和收集。
contentOwner: AG
mini-toc-levels: 1
feature: Collections,Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 23%

---

# 管理收藏集 {#manage-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=en) |
| AEM as a Cloud Service | 本文 |

集合是Adobe Experience Manager資產中的一組資產。 使用收藏集可在用户之间共享资源。集合可以是靜態集合或基於搜尋結果的動態集合。

收藏集与文件夹的不同之处是可包含来自不同位置的资源。您可以與獲指派不同許可權層級的不同使用者共用集合，包括檢視、編輯等。

您可以与一个用户共享多个收藏集。每个收藏集都包含对资源的引用。收藏集中会保持资源的引用完整性。

根據集合整理資產的方式，集合有下列型別：

* 包含資產、資料夾和其他集合的靜態參考清單的集合。

* 根據搜尋條件動態包含資產的智慧型集合。

## 存取集合主控台 {#navigate-the-collections-console}

若要開啟 **[!UICONTROL 集合]** 主控台：

若要開啟 **[!UICONTROL 集合]**，點選或按一下Experience Manager標誌。 從導覽頁面，前往 **[!UICONTROL 資產]** > **[!UICONTROL 集合]**.

## 创建收藏集 {#create-a-collection}

您可以使用以下任一專案建立集合： [靜態參考](#create-a-collection-with-static-references) 或根據 [搜尋條件型篩選器](#create-a-smart-collection). 您也可以從Lightbox建立集合。

### 建立具有靜態參照的集合 {#create-a-collection-with-static-references}

您可以建立具有靜態參照的集合，例如具有資產、資料夾、集合、迴轉集和影像集參照的集合。

1. 導覽至 **[!UICONTROL 集合]** 主控台。
1. 在工具列中點選/按一下 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立集合]** 頁面，輸入集合的標題和說明（選擇性）。
1. 向收藏集添加成员并分配相应的权限。或者，选择&#x200B;**[!UICONTROL 公共收藏集]**，以允许所有用户访问该收藏集。

   >[!NOTE]
   >
   >若要讓成員與其他使用者共用集合，請提供 `dam-users` 路徑下的群組讀取許可權 `home/users`. 將許可權授與使用者於 `/content/dam/collections` 可讓使用者在彈出式清單中檢視集合的位置。 或者，讓使用者成為 `dam-users` 群組。

1. （可選）為集合新增縮圖影像。
1. 点按／单 **[!UICONTROL 击创建]**，然后点按／单 **[!UICONTROL 击确定]** ，关闭对话框。 具有指定标题和属性的集合将在“收藏集”控制台中打开。

   >[!NOTE]
   >
   >Experience Manager Assets可讓您為集合建立稽核任務，其方式與為資產資料夾建立稽核任務類似。

   若要將資產新增至收藏集，請導覽至「資產」使用者介面。 如需詳細資訊，請參閱 [將資產新增至集合](#add-assets-to-a-collection).

### 使用dropzone建立集合 {#create-collections-using-dropzone}

您可以將資產從「資產」UI拖曳至收藏集。 您也可以建立收藏集的副本，並將資產拖曳至該處。

1. 從「資產」使用者介面中，選取您要新增至集合的資產。
1. 將資產拖曳至 **[!UICONTROL 放入集合]** 區域。 或者，點選/按一下 **[!UICONTROL 至集合]** 圖示加以檢視。
1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，点按/单击工具栏中的&#x200B;**[!UICONTROL 创建收藏集]**&#x200B;图标。如果要将资产添加到现有收藏集，请从页面中选择它，然后点按／单击添 **[!UICONTROL 加]**。 默认情况下，将选择最近更新的集合。
1. 在&#x200B;**[!UICONTROL 创建新收藏集]**&#x200B;对话框中，指定收藏集的名称。如果希望所有用户都可以访问该收藏集，请选择&#x200B;**[!UICONTROL 公共收藏集]**。
1. 點選/按一下 **[!UICONTROL 繼續]** 以建立集合。

### 建立智慧型集合 {#create-a-smart-collection}

Smart Collection會使用搜尋條件以動態方式填入資產。 您可以只使用檔案來建立Smart Collection，而不使用資料夾或檔案和資料夾。

1. 导航到资产UI，然后点按／单击搜 **[!UICONTROL 索图]** 标。
1. 在「全域搜尋」方塊中輸入搜尋關鍵字，然後選取 `Enter`. 點選/按一下「全域導覽」圖示以顯示「篩選器」面板，並從「搜尋」面板套用搜尋篩選器。
1. 從 **[!UICONTROL 檔案與資料夾]** 清單，選取 **[!UICONTROL 檔案]**.
1. 點選/按一下 **[!UICONTROL 儲存智慧型集合]**.
1. 指定集合的名稱。 選取 **[!UICONTROL 公用]** 將具有檢視器角色的DAM Users群組新增至智慧型集合。

   >[!NOTE]
   >
   >如果您選取 **[!UICONTROL 公用]**，在您建立智慧型集合後，擁有擁有擁有者角色的所有人都能使用該集合。 如果您取消 **[!UICONTROL 公用]** 選項，DAM使用者群組不再與智慧型集合相關聯。

1. 点按/单击&#x200B;**[!UICONTROL 保存]**，以创建智能收藏集，然后关闭消息框以完成该进程。新的智能收藏集也会添加到&#x200B;**[!UICONTROL 保存的搜索]**列表。.
“创建智能选 **[!UICONTROL 择”按钮的标签会变]** 为“编 **[!UICONTROL 辑智能选择”]**。 要编辑智能收藏集的设置，请从“文件和文 **[!UICONTROL 件夹]** ”列 **[!UICONTROL 表中选择“文件]** ”。 然后，点按／单击编辑 **[!UICONTROL 智能选择]** 按钮。

## 将资源添加到收藏集 {#add-assets-to-a-collection}

您可以將資產新增至包含參照資產或資料夾清單的集合。

>[!NOTE]
>
>智慧型集合會使用搜尋查詢來填入資產。 因此，資產和資料夾的靜態參考並不適用於它們。

1. 在Assets UI中，導覽至您要新增至集合的資產位置。
1. 選取資產，然後點選/按一下 **[!UICONTROL 至集合]** 圖示加以檢視。 或者，您可以將資產拖曳至 **[!UICONTROL 放入集合]** 區域。 拖放區域啟動且標籤變更為時，放開滑鼠按鈕 **[!UICONTROL 放置以新增]**.
1. 在 **[!UICONTROL 新增至集合]** 頁面上，選取您要新增資產的集合。
1. 點選/按一下 **[!UICONTROL 新增]**，然後關閉確認訊息。 資產會新增至集合。

## 編輯智慧型集合 {#edit-a-smart-collection}

智慧型集合是透過儲存搜尋來建置，因此您可以修改的搜尋引數來變更其內容 [已儲存的搜尋](#saved-searches).

1. 在「資產」使用者介面中，點選/按一下 **[!UICONTROL 搜尋]** 圖示加以檢視。
1. 將游標放在Omnisearch方塊中，選取 `Enter` 金鑰。
1. 點選/按一下「全域導覽」圖示，以顯示「篩選器」面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，选择要修改的智能收藏集。“搜索”面板显示为保存的搜索配置的过滤器。
1. 從 **[!UICONTROL 檔案與資料夾]** 清單，選取 **[!UICONTROL 檔案]**.
1. 視需要修改一或多個篩選器。 點選/按一下 **[!UICONTROL 編輯智慧型集合]**. 您也可以編輯智慧型集合的名稱。
1. 點選/按一下 **[!UICONTROL 儲存]**. 此 **[!UICONTROL 編輯智慧型集合]** 對話方塊隨即顯示。
1. 點選/按一下 **[!UICONTROL 覆寫]** 將原始的智慧型集合取代為已編輯的集合。 或者，選取 **[!UICONTROL 另存為]** 以個別儲存已編輯的集合。
1. 在確認對話方塊中，點選/按一下 **[!UICONTROL 儲存]** 以完成程式。

## 查看和编辑收藏集元数据 {#view-and-edit-collection-metadata}

收藏集中繼資料包含有關收藏集的資料，包括新增的任何標籤。

1. 從「系列」控制檯中，選取系列，然後點選/按一下 **[!UICONTROL 屬性]** 圖示加以檢視。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，从&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**高级**&#x200B;选项卡中查看收藏集元数据。
1. 視需要修改中繼資料，然後點選/按一下 **[!UICONTROL 儲存並關閉]** 以儲存變更。

### 大量編輯收藏集中繼資料 {#edit-collection-metadata-in-bulk}

您可以同時編輯多個集合的中繼資料。 此功能可協助您在多個集合中快速復寫常見的中繼資料。

1. 在「收藏集」控制檯中，選取您要編輯中繼資料的兩個或多個收藏集。
1. 在工具列中，點選/按一下 **[!UICONTROL 屬性]** 圖示。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，根据需要编辑&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡下的元数据。
1. 點選/按一下 **[!UICONTROL 儲存並關閉]** ，然後關閉確認對話方塊以完成此程式。
1. 要将新元数据附加到现有元数据，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。点按/单击&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >“追加模式”仅适用于可包含多个值的字段。对于只能包含单个值的字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 搜索 {#searching}

集合中的搜尋功能支援兩者 [搜尋集合](#search-collections) 和 [在集合中搜尋資產](#search-within-collections).

### 搜尋集合 {#search-collections}

您可以從「集合」控制檯搜尋集合。 當您在Omnisearch方塊中使用關鍵字搜尋時， [!DNL Experience Manager Assets] 會搜尋系列名稱、中繼資料和新增至系列的標籤。

如果您從最上層搜尋集合，搜尋結果中只會傳回個別集合。 會排除收藏集中的資產或資料夾。 在所有其他情況下（例如，在個別集合或資料夾階層中），都會傳回所有相關資產、資料夾和集合。

### 在集合中搜尋 {#search-within-collections}

在「集合」控制檯中，點選/按一下集合以將其開啟。

在集合中， [!DNL Experience Manager] 搜尋僅限於您檢視之集合中的資產（及其標籤和中繼資料）。 在資料夾中搜尋時，會傳回目前資料夾中所有相符的資產和子資料夾。 您在集合中搜尋時，只會傳回相符的資產、資料夾和屬於集合直接成員的其他集合。

## 編輯集合設定 {#edit-collection-settings}

您可以編輯收藏集設定（例如標題和說明），或將成員新增至收藏集。

1. 選取系列，然後點選/按一下 **[!UICONTROL 設定]** 圖示加以檢視。 或者，使用 **[!UICONTROL 設定]** 集合縮圖中的快速動作。
1. 在&#x200B;**[!UICONTROL 收藏集设置]**&#x200B;页面中修改收藏集设置。例如，按照[添加收藏集](#create-a-collection)中所述修改收藏集标题、描述、成员和权限。
1. 點選/按一下 **[!UICONTROL 儲存]** 以儲存變更。

## 删除收藏集 {#delete-a-collection}

1. 從「系列」控制檯中，選取一或多個系列，然後點選/按一下工具列中的刪除圖示。
1. 在對話方塊中，點選/按一下 **[!UICONTROL 刪除]** 以確認刪除動作。

   >[!NOTE]
   >
   >您也可以刪除智慧型集合，方法是 [刪除已儲存的搜尋](#saved-searches).

## 下载收藏集 {#download-a-collection}

下載集合時，會下載集合中資產的整個階層，包括資料夾和子集合。

1. 從「集合」控制檯中，選取一或多個要下載的集合。
1. 在工具列中，點選/按一下下載圖示。
1. 在 **[!UICONTROL 下載]** 對話方塊，點選/按一下 **[!UICONTROL 下載]**. 如果您想要下載收藏集中資產的轉譯，請選取 **[!UICONTROL 轉譯]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   當您選取要下載的集合時，將會下載集合下的完整資料夾階層。 若要將您下載的每個收藏集（包括父收藏集巢狀下子收藏集中的資產）納入個別資料夾，請選取 **[!UICONTROL 為每個資產建立個別的資料夾]**.

## 編輯多個集合的中繼資料屬性 {#editing-metadata-properties-of-multiple-collections}

AdobeEnterprise Manager資產可讓您大量編輯許多集合的中繼資料。 使用 [!UICONTROL 屬性] 頁面，對多個集合執行中繼資料變更，例如，將中繼資料屬性變更為通用值，或新增或修改標籤。

若要自訂中繼資料 [!UICONTROL 屬性] 頁面，包括新增、修改、刪除中繼資料屬性，請使用結構描述編輯器。

>[!NOTE]
>
>大量編輯方法適用於集合中可用的資產。 對於跨資料夾可用的資產或符合共同條件的資產，可以 [搜尋後大量更新中繼資料](/help/assets/search-assets.md#metadata-updates).

1. 在集合控制檯中，選取您要編輯的集合。
1. 在工具列中點選/按一下 **[!UICONTROL 屬性]** 以開啟 [!UICONTROL 屬性] 所選集合的頁面。
1. 修改各種標籤下所選集合的中繼資料屬性。

   >[!NOTE]
   >
   >您為所選集合新增的中繼資料會覆寫這些集合先前的中繼資料，但標籤除外。 您在中新增的任何標籤 **[!UICONTROL 標籤]** 欄位)會附加至中繼資料中的現有標籤清單。

1. 若要檢視特定集合的中繼資料屬性，請取消選取集合清單中剩餘的集合。 中繼資料編輯器欄位會填入特定集合的中繼資料。

   >[!NOTE]
   >
   >* 在集合屬性頁面中，您可以取消選取範圍，從集合清單中移除集合。 集合清單預設會選取所有集合。 您移除的集合中繼資料未更新。
   >* 在清單頂端，選取附近的核取方塊 **[!UICONTROL 標題]** 在選取集合和清除清單之間切換。


1. 保存更改。

## 建立巢狀集合 {#create-nested-collections}

您可以將集合新增至另一個集合，藉此建立巢狀集合。

1. 從「系列」控制檯中，選取所需的系列或系列群組，然後點選或按一下 **[!UICONTROL 至集合]** （在工具列中）。
1. 從 **[!UICONTROL 新增至集合]** 頁面上，選取要新增集合的集合。

   >[!NOTE]
   >
   >根據預設，系統會選取最近更新的集合，位於 **[!UICONTROL 新增至集合]** 頁面。

1. 點選/按一下 **[!UICONTROL 新增]**. 訊息會確認此集合已新增至中的目標集合。 **[!UICONTROL 選取目的地]** 頁面。 關閉訊息以完成程式。

>[!NOTE]
>
>無法巢狀化智慧型集合。 換言之，智慧型集合不能包含任何其他集合。

## 保存的搜索 {#saved-searches}

在“资产”用户界面中，您可以根据某些规则、搜索条件或自定义搜索彩块化来搜索或筛选资产。 如果将这些搜索另存为&#x200B;**[!UICONTROL 保存的搜索]**，则以后可以从“过滤器”面板的&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中访问它们。 创建保存的搜索也会创建智能收藏集。

创建智能收藏集时将创建保存的搜索。智能收藏集会自动添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。收藏集的“保存的搜索”查询将保存在 `dam:query` CRXDE 的属性中的相对位置`/content/dam/collections/`。您可以儲存的搜尋以及清單中顯示的已儲存搜尋沒有限制。

>[!NOTE]
>
>您可以使用與共用靜態集合相同的方式共用智慧型集合。

編輯已儲存的搜尋與編輯智慧型集合相同。 如需詳細資訊，請參閱 [編輯智慧型集合](#edit-a-smart-collection).

若要刪除已儲存的搜尋，請遵循下列步驟：

1. 在Assets使用者介面中，點選/按一下工具列中的搜尋圖示。

1. 將游標放在Omnisearch欄位中，選取 `Enter` 金鑰。
1. 按一下或點選「全域導覽」圖示以顯示「篩選器」面板。
1. 从保存 **[!UICONTROL 的搜索列表]** ，点按／单 **** 击要删除的智能收藏集旁边的删除。
1. 在對話方塊中，點選/按一下 **[!UICONTROL 刪除]** 以刪除儲存的搜尋。

## 對集合執行工作流程 {#run-a-workflow-on-a-collection}

您可以為集合中的資產執行工作流程。 如果集合包含巢狀集合，工作流程也會在巢狀集合內的資產上執行。 不過，如果集合和巢狀集合包含重複資產，工作流程只會針對此類資產執行一次。

1. 從「集合」控制檯中，選取您要執行工作流程的集合。
1. 點選/按一下「全域導覽」圖示，然後選擇 **[!UICONTROL 時間表]** 從清單中。
1. 在時間軸中，選取或點選底部的脫字元號圖示，然後點選/按一下 **[!UICONTROL 開始工作流程]**.
1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;部分，从列表中选择工作流模型。例如，选择 **[!UICONTROL DAM 更新资产]**&#x200B;模型。
1. 輸入工作流程的標題，然後點選/按一下 **[!UICONTROL 開始]**.
1. 在對話方塊中，點選/按一下 **[!UICONTROL 繼續]**. 工作流程會在集合中的所有資產上執行。

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
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [建立集合的稽核任務](/help/assets/bulk-approval.md)

