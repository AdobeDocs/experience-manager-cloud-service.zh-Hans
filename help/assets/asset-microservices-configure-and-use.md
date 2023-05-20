---
title: 設定和使用資產微服務
description: 設定並使用雲端原生資產微服務，以大規模處理資產。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 3%

---

# 使用資產微服務和處理設定檔 {#get-started-using-asset-microservices}

資產微服務可使用雲端原生應用程式（也稱為背景工作），提供可擴充及具彈性的資產處理功能。 Adobe會管理服務，以最佳方式處理各種資產型別和處理選項。

資產微服務可讓您處理 [廣泛的檔案型別](/help/assets/file-format-support.md) 比舊版更豐富的現成可用格式 [!DNL Experience Manager]. 例如，現在可以提取PSD和PSB格式的縮圖，但之前需要第三方解決方案，例如 [!DNL ImageMagick].

資產處理方式取決於中的設定 **[!UICONTROL 處理設定檔]**. Experience Manager提供基本的預設設定，並可讓管理員新增更具體的資產處理設定。 管理員可建立、維護和修改後處理工作流程的設定，包括可選的自訂。 自訂工作流程可讓開發人員擴充預設選件。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![資產處理的高層級檢視](assets/asset-microservices-flow.png "資產處理的高層級檢視")

>[!NOTE]
>
>此處說明的資產處理會取代 `DAM Update Asset` 舊版中存在的工作流程模型 [!DNL Experience Manager]. 大多數標準轉譯產生和中繼資料相關步驟已由資產微服務處理取代，而其餘步驟（如有）可由後處理工作流程設定取代。

## 瞭解資產處理選項 {#get-started}

[!DNL Experience Manager] 允許進行下列層級的處理。

| 选项 | 描述 | 涵蓋的使用案例 |
|---|---|---|
| [默认配置](#default-config) | 目前可用，無法修改。 此設定提供非常基本的轉譯產生功能。 | <ul> <li>使用的標準縮圖 [!DNL Assets] 使用者介面（48、140和319畫素） </li> <li> 大型預覽（網頁轉譯 — 1280畫素） </li><li> 中繼資料和文字擷取。</li></ul> |
| [自訂設定](#standard-config) | 由管理員透過使用者介面設定。 延伸預設選項，為產生轉譯提供更多選項。 擴充現成的選項，以提供不同的格式和轉譯。 | <ul><li>FPO轉譯。 </li> <li>變更檔案格式和影像解析度</li> <li> 有條件地套用至已設定的檔案型別。 </li> </ul> |
| [自訂設定檔](#custom-config) | 管理員透過使用者介面設定為透過自訂應用程式使用自訂程式碼來呼叫 [asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). 以雲端原生且可擴充的方法支援更複雜的需求。 | 另請參閱 [允許的使用案例](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支持的文件格式 {#supported-file-formats}

資產微服務可支援多種檔案格式來處理、產生轉譯或擷取中繼資料。 另請參閱 [支援的檔案格式](file-format-support.md) 以取得MIME型別的完整清單，以及每種型別支援的功能。

## 默认配置 {#default-config}

已預先設定一些預設值，以確保Experience Manager中所需的預設轉譯可供使用。 預設設定也會確保中繼資料擷取和文字擷取作業可供使用。 使用者可以立即開始上傳或更新資產，且預設可使用基本處理。

使用預設設定時，只會設定最基本的處理設定檔。 使用者介面上看不到此類處理設定檔，且您無法對其進行修改。 它一律會執行以處理上傳的資產。 此類預設處理設定檔可確保以下專案所需的基本處理： [!DNL Experience Manager] 在所有資產上完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 標準設定 {#standard-config}

[!DNL Experience Manager] 根據使用者的需求，提供可針對常見格式產生更特定轉譯的功能。 管理員可以建立其他 [!UICONTROL 處理設定檔] 以方便這類轉譯的建立。 然後，使用者將一個或多個可用的設定檔指派給特定資料夾，以完成其他處理。 舉例來說，其他處理可產生網頁、行動裝置和平板電腦的轉譯。 以下影片說明如何建立和套用 [!UICONTROL 處理設定檔] 以及如何存取建立的轉譯。

* **轉譯寬度和高度**：轉譯寬度和高度規格提供所產生輸出影像的最大大小。 資產微服務會嘗試產生最大可能的轉譯，其寬度和高度分別不會大於指定的寬度和高度。 外觀比例會保留，與原始外觀比例相同。 空白值表示資產處理會假設原始畫面的畫素尺寸。

* **MIME型別包含規則**：處理具有特定MIME型別的資產時，會先根據轉譯規格的排除MIME型別值檢查MIME型別。 如果它符合該清單，則不會為資產（封鎖清單）產生此特定轉譯。 否則，會根據包含的MIME型別檢查MIME型別，如果它符合清單，則會產生轉譯（允許清單）。

* **特殊FPO轉譯**：從放置大型資產時 [!DNL Experience Manager] 到 [!DNL Adobe InDesign] 檔案，之後創意專業人士會等待相當長的時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，已封鎖該使用者，不允許使用 [!DNL InDesign]. 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe可暫時將小型轉譯置於 [!DNL InDesign] 開始使用的檔案，稍後可隨選以完整解析度資產取代。 [!DNL Experience Manager] 提供僅用於放置的轉譯(FPO)。 這些FPO轉譯檔案大小雖小，但外觀比例相同。

處理設定檔可包含FPO （僅供刊登）轉譯。 另請參閱 [!DNL Adobe Asset Link] [檔案](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 以瞭解您是否必須為處理設定檔開啟此功能。 如需詳細資訊，請參閱 [AdobeAsset Link完整檔案](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html).

### 建立標準設定檔 {#create-standard-profile}

若要建立標準處理設定檔，請遵循下列步驟：

1. 管理員存取權 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**. 单击&#x200B;**[!UICONTROL 创建]**。
1. 提供可協助您在套用至資料夾時唯一識別設定檔的名稱。
1. 若要產生FPO轉譯，請前往 **[!UICONTROL 影像]** 標籤，啟用 **[!UICONTROL 建立FPO轉譯]**. 輸入 **[!UICONTROL 品質]** 值介於1到100之間。
1. 若要產生其他轉譯，請按一下 **[!UICONTROL 新增]** 並提供下列資訊：

   * 每個轉譯的檔案名稱。
   * 每個轉譯的檔案格式(PNG、JPEG、GIF或WebP)。
   * 每個轉譯的寬度和高度（畫素）。 如果未指定值，則會使用原始影像的完整畫素大小。
   * 每個JPEG和WebP轉譯的品質（百分比）。
   * 包含和排除MIME型別以定義設定檔的適用性。

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. 单击“**[!UICONTROL 保存]**”。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自訂設定檔和使用案例 {#custom-config}

此 [!DNL Asset Compute Service] 支援各種使用案例，例如預設處理、處理Adobe專用格式(如Photoshop檔案)以及實作自訂或組織專用處理。 過去需要的DAM更新資產工作流程自訂可自動處理，或透過處理設定檔設定來處理。 如果這些處理選項無法滿足業務需求，Adobe建議開發並使用 [!DNL Asset Compute Service] 以延伸預設功能。 如需概覽，請參閱 [瞭解擴充功能及使用時機](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe建議只有在無法使用預設設定或標準設定檔滿足業務需求時，才使用自訂應用程式。

它可以將影像、視訊、檔案和其他檔案格式轉換為不同的轉譯專案，包括縮圖、擷取的文字和中繼資料以及封存。

開發人員可使用 [!DNL Asset Compute Service] 至 [建立自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) 適用於支援的使用案例。 [!DNL Experience Manager] 可使用管理員設定的自訂設定檔，從使用者介面呼叫這些自訂應用程式。 [!DNL Asset Compute Service] 支援以下叫用外部服務的使用案例：

* 使用 [!DNL Adobe Photoshop]的 [ImageCutout API](https://developer.adobe.com/photoshop/photoshop-api-docs/) 並將結果儲存為轉譯。
* 呼叫第三方系統以更新資料，例如PIM系統。
* 使用 [!DNL Photoshop] 根據Photoshop範本產生多種轉譯的API。
* 使用 [ADOBE LIGHTROOM API](https://developer.adobe.com/photoshop/photoshop-api-docs/) 以最佳化所擷取的資產，並將它們儲存為轉譯。

>[!NOTE]
>
>您無法使用自訂應用程式編輯標準中繼資料。 您只能修改自訂中繼資料。

### 建立自訂設定檔 {#create-custom-profile}

若要建立自訂設定檔，請遵循下列步驟：

1. 管理員存取權 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**. 单击&#x200B;**[!UICONTROL 创建]**。
1. 按一下 **[!UICONTROL 自訂]** 標籤。 按一下 **[!UICONTROL 新增]**. 提供所需的轉譯檔案名稱。
1. 提供以下信息。

   * 每個轉譯的檔案名稱和支援的副檔名。
   * [App Builder自訂應用程式的端點URL](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). 應用程式必須來自與Experience Manager帳戶相同的組織。
   * 將服務引數新增至 [將額外的資訊或引數傳遞至自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * 包含和排除MIME型別，以將處理限製為一些特定的檔案格式。

   单击“**[!UICONTROL 保存]**”。

自訂應用程式為Headless [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/) 應用程式。 如果您的自訂應用程式設定了處理設定檔，則會取得所有提供的檔案。 應用程式必須篩選檔案。

>[!CAUTION]
>
>如果App Builder應用程式和 [!DNL Experience Manager] 帳戶並非來自相同組織，整合無法運作。

### 自訂設定檔的範例 {#custom-profile-example}

為了說明自訂設定檔的使用情況，讓我們考慮使用案例，將一些自訂文字套用至行銷活動影像。 您可以建立處理設定檔，以利用Photoshop API來編輯影像。

asset compute服務整合可讓Experience Manager使用這些引數傳遞給自訂應用程式。 [!UICONTROL 服務引數] 欄位。 自訂應用程式接著會呼叫Photoshop API，並將這些值傳遞至API。 例如，您可以傳遞字型名稱、文字顏色、文字粗細和文字大小，以將自訂文字新增至行銷活動影像。

<!-- TBD: Check screenshot against the interface. -->

![custom-processing-profile](assets/custom-processing-profile.png)

*圖：使用 [!UICONTROL 服務引數] 將新增資訊傳遞至預先定義引數（內建至自訂應用程式）的欄位。 在此範例中，上傳行銷活動影像時，影像會以下列專案更新： `Jumanji` 文字輸入 `Arial-BoldMT` 字型。*

## 使用處理設定檔來處理資產 {#use-profiles}

建立其他自訂處理設定檔並套用至特定資料夾，以便Experience Manager處理上傳至這些資料夾或更新之資產。 系統會一律執行預設的內建標準處理設定檔，但不會顯示在使用者介面上。 如果您新增自訂設定檔，則會使用兩個設定檔來處理上傳的資產。

使用下列其中一種方法，將處理設定檔套用至資料夾：

* 管理員可以在以下位置選擇處理設定檔定義： **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 處理設定檔]**，並使用 **[!UICONTROL 將設定檔套用至資料夾]** 動作。 它會開啟內容瀏覽器，讓您導覽至特定資料夾、選取資料夾並確認設定檔的應用。
* 使用者可以在Assets使用者介面中選取資料夾，使用 **[!UICONTROL 屬性]** 動作若要開啟資料夾屬性畫面，請按一下 **[!UICONTROL 資產處理]** 標籤，然後在 [!UICONTROL 處理設定檔] 清單中，為該資料夾選取適當的處理設定檔。 要保存更改，请单击&#x200B;**[!UICONTROL “保存并关闭”]**。
   ![從「資產屬性」索引標籤將處理設定檔套用至資料夾](assets/folder-properties-processing-profile.png)

* 使用者可以在Assets使用者介面中選取資料夾或特定資產，以套用處理設定檔，然後選取 ![資產重新處理圖示](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL 重新處理資產]** 從上方可用的選項中選取。

>[!TIP]
>
>一个文件夹只能应用一个处理配置文件。若要產生更多轉譯，請將更多轉譯定義新增至現有的處理設定檔。

在處理設定檔套用至資料夾後，系統會使用設定的其他處理設定檔來處理此資料夾或其任何子資料夾中上傳（或更新）的所有新資產。 这种处理是在标准默认配置文件之外进行的。

>[!NOTE]
>
>套用至資料夾的處理設定檔適用於整個樹狀結構，但可以覆寫套用至子資料夾的其他設定檔。 將資產上傳至資料夾時，Experience Manager會檢查包含資料夾的屬性以取得處理設定檔。 如果未应用任何配置文件，则会检查层级中的父文件夹以确定要应用的处理配置文件。

若要確認資產已處理，請在以下位置預覽產生的轉譯： [!UICONTROL 轉譯] 在左側邊欄中檢視。 開啟資產預覽並開啟左側邊欄以存取 **[!UICONTROL 轉譯]** 檢視。 處理設定檔中的特定轉譯（其特定資產型別符合MIME型別包含規則）應是可見且可存取的。

![其他轉譯](assets/renditions-additional-renditions.png)

*圖：由套用至父資料夾的處理設定檔產生的兩個額外轉譯範例。*

## 後處理工作流程 {#post-processing-workflows}

若是需要額外處理無法使用處理設定檔實現的資產，可將其他後處理工作流程新增到設定。 後處理可讓您在使用資產微服務的可設定處理之上新增完全自訂的處理作業。

後處理工作流程，或 [自動啟動工作流程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html)，如果已設定，則會自動執行 [!DNL Experience Manager] 微服務處理完成後。 不需要手動新增工作流程啟動器來觸發工作流程。 範例包括：

* 處理資產的自訂工作流程步驟。
* 整合以將中繼資料或屬性從外部系統新增至資產，例如產品或程式資訊。
* 外部服務完成的其他處理。

若要將後處理工作流程設定新增至 [!DNL Experience Manager]，請遵循下列步驟：

* 建立一或多個工作流程模型。 這些自訂模型稱為 *後處理工作流程模型* 在本檔案內。 這些是正常的 [!DNL Experience Manager] 工作流程模型。
* 將所需的工作流程步驟新增至這些模型。 檢閱預設工作流程的步驟，並將所有必要的預設步驟新增至自訂工作流程。 這些步驟會根據工作流程模型設定在資產上執行。 例如，如果您想在資產上傳時自動進行智慧標籤，請將步驟新增至自訂後處理工作流程模型。
* 新增 [!UICONTROL DAM更新資產工作流程已完成程式] 在結尾處步驟。 新增此步驟可確保Experience Manager知道處理何時結束，且資產可標示為已處理，即 *新增* 會顯示在資產上。
* 建立「自訂工作流程執行器」服務的設定，允許透過路徑（資料夾位置）或規則運算式設定後置處理工作流程模型的執行。

如需後處理工作流程中可以使用哪些標準工作流程步驟的詳細資訊，請參閱 [後處理工作流程中的工作流程步驟](developer-reference-material-apis.md#post-processing-workflows-steps) （在開發人員參考中）。

### 建立後處理工作流程模型 {#create-post-processing-workflow-models}

後處理工作流程模型為一般模型 [!DNL Experience Manager] 工作流程模型。 如果您需要對不同的存放庫位置或資產型別進行不同的處理，請建立不同的模型。

處理步驟會視需要新增。 您可以使用這兩者、可用的支援步驟，以及任何自訂實作的工作流程步驟。

確定每個後處理工作流程的最後一步為 `DAM Update Asset Workflow Completed Process`. 最後一步有助於確保Experience Manager知道資產處理何時完成。

### 設定後處理工作流程執行 {#configure-post-processing-workflow-execution}

資產微服務完成上傳資產的處理之後，您可以定義後續處理工作流程以進一步處理資產。 若要使用工作流程模型設定後續處理，您可以執行下列任一項作業：

* [在資料夾屬性中套用工作流程模型](#apply-workflow-model-to-folder).
* [設定自訂工作流程執行器服務](#configure-custom-workflow-runner-service).

#### 將工作流程模型套用至資料夾 {#apply-workflow-model-to-folder}

對於典型的後續處理使用案例，請考慮使用將工作流程套用至資料夾的方法。 若要在資料夾中套用工作流程模型 [!UICONTROL 屬性]，請遵循下列步驟：

1. 建立工作流程模型。
1. 選取資料夾，按一下 **[!UICONTROL 屬性]** ，然後按一下 **[!UICONTROL 資產處理中]** 標籤。
1. 下 **[!UICONTROL 自動啟動工作流程]**，選取所需的工作流程、提供工作流程的標題，然後儲存變更。

   ![將後處理工作流程套用至其屬性中的資料夾](assets/post-processing-profile-workflow-for-folders.png)

#### 設定自訂工作流程執行器服務 {#configure-custom-workflow-runner-service}

您可以為無法透過將工作流程套用至資料夾來輕鬆完成的進階設定設定設定自訂工作流程執行器服務。 例如，使用規則運算式的工作流程。 Adobe CQ DAM自訂工作流程執行器(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是一項OSGi服務。 它提供下列兩個設定選項：

* 依路徑分類的處理後工作流程(`postProcWorkflowsByPath`)：可以根據不同的存放庫路徑列出多個工作流程模型。 使用冒號分隔路徑和模型。 支援簡單的存放庫路徑。 將這些專案對應至中的工作流程模型 `/var` 路徑。 例如：`/content/dam/my-brand:/var/workflow/models/my-workflow`。
* 依據運算式的後處理工作流程(`postProcWorkflowsByExpression`)：可根據不同的規則運算式列出多個工作流程模型。 運算式和模型應以冒號分隔。 規則運算式應直接指向Asset節點，而非轉譯或檔案之一。 例如：`/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`。

若要瞭解如何部署OSGi設定，請參閱 [部署至 [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### 停用後處理工作流程執行

當不需要後期處理時，請在中建立並使用「空」工作流程模型 __自動啟動工作流程__ 選取。

##### 建立停用的自動啟動工作流程模型

1. 導覽至 __「工具」>「工作流程」>「模型」__
1. 選取 __「建立」>「建立模型」__ 形成頂端動作列
1. 提供新工作流程模型的標題和名稱，例如：
   * 標題：停用自動啟動工作流程
   * 名稱： disable-auto-start-workflow
1. 選取 __完成__ 建立工作流程模型的方式
1. __選取__ 和 __編輯__ 新建立的工作流程模型
1. 在工作流程模型編輯器中，選擇 __步驟1__ 從模型定義中刪除它
1. 開啟 __側面板__，並選取 __步驟__
1. 拖曳 __DAM更新資產工作流程已完成__ 逐步執行模型定義
1. 選取 __頁面資訊__ 按鈕(在 __側面板__ 切換)，然後選取 __開啟屬性__
1. 在 __基本__ 索引標籤，選取 __暫時性工作流程__
1. 選取 __儲存並關閉__ 從頂端動作列
1. 選取 __同步__ 在頂端動作列中
1. 關閉工作流程模型編輯器

##### 套用停用的自動啟動工作流程模型

請依照中概述的步驟操作 [將工作流程模型套用至資料夾](#apply-workflow-model-to-folder) 並設定 __停用自動啟動工作流程__ 作為 __自動啟動工作流程__ 資料夾不需要資產後處理。

## 最佳作法和限制 {#best-practices-limitations-tips}

* 在設計工作流程時，請考慮您對所有型別轉譯的需求。 如果您預計未來不需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長時間使用後，不需要的轉譯可能會佔用大量儲存空間 [!DNL Experience Manager]. 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂 [!DNL Experience Manager] 以刪除特定轉譯或刪除資產，然後再次上傳這些資產。
* 目前，支援僅限於產生轉譯。 不支援產生新資產。
* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳超大型資產時，有時中繼資料擷取作業會失敗。

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

>[!MORELIKETHIS]
>
>* [asset compute服務簡介](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [瞭解擴充功能及使用時機](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [如何建立自訂應用程式](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html).
>* [各種使用案例支援的MIME型別](/help/assets/file-format-support.md).


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
