---
title: 整合的最佳實務 [!DNL Adobe Creative Cloud]
description: 最佳實務可將Experience Manager部署與Adobe Creative Cloud整合，以簡化資產轉移工作流程，並實現最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '3495'
ht-degree: 16%

---

# Adobe Experience Manager與Creative Cloud整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

Adobe Experience Manager Assets是數位資產管理(DAM)解決方案，可與Adobe Creative Cloud整合，以協助DAM使用者與創意團隊合作，精簡內容建立過程中的共同作業。

Adobe Creative Cloud為創意團隊提供解決方案和服務的生態系統，以協助他們建立數位資產。 其中包括案頭和行動應用程式、雲端服務（例如具備案頭同步處理或網頁體驗的儲存空間），以及Adobe Stock等行銷場所。

請閱讀下文，瞭解根據您的使用案例，在案頭版和企業級DAM之間選擇哪些整合，以及哪些是連線工作流程的相關最佳實務。

>[!NOTE]
>
>Creative Cloud資料夾共用的Experience Manager現已棄用，不再涵蓋於下方。 Adobe建議使用Adobe Asset Link或Experience Manager案頭應用程式等較新功能，以便創意使用者能存取Experience Manager管理的資產。

## 創意人員、行銷人員和DAM使用者的共同作業需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化創意人員在桌上型電腦上的體驗 | 簡化從DAM存取資產的程式([!DNL Assets])適用於創意專家，或更廣義地說，適用於在原生資產建立應用程式中工作的案頭使用者。 他們需要一種簡單明瞭的方式，來探索、使用（開啟）、編輯和儲存對Experience Manager的變更，以及上傳新檔案。 | Win或Mac桌上型電腦；Creative Cloud應用程式 |
| 提供高品質、現成可用的資產，來自 [!DNL Adobe Stock] | 行銷人員可協助資產來源和探索，以加速內容建立流程。 創意專業人士可從其創意工具內直接使用核准的資產。 | [!DNL Assets]； [!DNL Adobe Stock] 市集；中繼資料欄位 |
| 依組織分送和共用資產 | 內部部門/當地分支和外部合作夥伴、經銷商和代理商會使用上級組織共用的已核准資產。 企業想要安全且順暢地共用建立的資產，以更廣泛地重複使用。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| 自動產生已上傳資產的預先定義變化 | 運用Adobe獨特的媒體處理和轉換技術，針對預先定義的動作自動處理資產。 建立自訂邏輯，以使用API和資產微服務定義您自己的動作。 | [!DNL Assets] 用户界面 |

## 支援協同合作需求的Adobe方案 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe方案 | 相關曲面 |
|---|---|---|
| 創意使用者從中發現資產 [!DNL Experience Manager]，開啟並使用它們、編輯和上傳變更至 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager]，而不需離開其 [!DNL Creative Cloud] 應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign。 |
| 企業使用者可簡化資產的開啟與使用、編輯與上傳變更 [!DNL Experience Manager]，並將新檔案上傳至 [!DNL Experience Manager] 從案頭環境。 他們使用一般整合在原生案頭應用程式中開啟任何資產型別，包括非Adobe的資產型別。 | [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 在Win和Mac案頭上Experience Manager案頭應用程式 |
| 行銷人員和商務使用者可在Experience Manager中探索、預覽、授權並儲存及管理Adobe Stock資產。 授權和儲存的資產可提供精選Adobe Stock中繼資料，以改善治理。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網頁介面 |
| 改善數位產品設計師和行銷人員之間的協同合作。 讓設計人員在Adobe XD畫布上的設計和線框模型中使用數位資產。 |  [!DNL Adobe XD] 的 [[!DNL Adobe Asset Link] ](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| 行銷人員可以根據上傳的資產和使用自訂建立的預先定義動作，自動建立變數和衍生工具。 使用此自動化功能來改善內容速度並減少手動操作。 | [內容自動化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] 網頁介面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。替代解決方案，例如 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可建置在 [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) 元件， [連結共用](share-assets.md)，使用 [Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md) 應根據特定需求審查。

![Experience Manager的Creative Cloud連線：決定要使用哪個功能](assets/creative-connections-aem.png)

決定要使用哪種功能

### 使用案例與Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

| 使用案例 | Adobe Asset Link | Experience Manager 桌面应用程序 | 備註或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 探索 — 瀏覽資料夾 | 是 | Experience ManagerWeb UI +案頭動作 | 瀏覽網路共用時，請關閉縮圖以避免下載資產的二進位檔案。 |
| 探索 — 存取集合 | 是 | Experience ManagerWeb UI +案頭動作 |  |
| 探索 — 搜尋資產 | 是 | Experience ManagerWeb UI +案頭動作 |  |
| 使用 — 開啟資產 | 是 | 是 — 適用於任何應用程式 | [從Web介面開啟](/help/assets/manage-digital-assets.md#previewing-assets) 或從Finder |
| 使用 — 將資產從Experience Manager置入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | Experience Manager案頭應用程式可讓您存取本機檔案系統上的資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟動作（在網路共用中） | [在AAL中籤出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 預設會將資產儲存至使用者的creative cloud儲存體帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — 在Experience Manager外部進行中的工作 | 是 — 使用者的Creative Cloud儲存帳戶中可用的資產，已同步至案頭。 | 是 |  |
| 編輯 — 上傳變更 | 是 —  [簽入動作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 含選擇性註解 | 是 |  |
| 上傳 — 單一檔案 | 是 — 上傳目前作用中的檔案 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](/help/assets/manage-digital-assets.md#uploading-assets)；自訂指令碼或工具 |
| 其他 — 使用者和登入 | 可辨識登入Creative Cloud案頭應用程式的Creative Cloud使用者(SSO) | Experience Manager使用者/登入 | 這兩個解決方案的使用者都會計入Experience Manager的使用者配額。 |
| 雜項 — 網路與存取 | 需要從使用者的案頭存取以透過網路Experience Manager部署 | 需要從使用者的案頭存取以透過網路Experience Manager部署 | Adobe資產連結不共用網路Proxy環境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

若要支援資產散佈使用案例，請考量下列選項：

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於可設定的Assets附加元件以發佈資產。

* 自訂解決方案是根據 [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) 程式碼基底。
* Experience Manager [連結共用](/help/assets/share-assets.md) 使用連結臨機共用資產。
* [Assets網頁介面](/help/assets/manage-digital-assets.md) 外部合作方的區域由Experience Manager存取控制設定保護，並輔以必要的IT/網路組態調整，讓這些外部使用者能夠存取Experience Manager。

## 重要概念與使用案例 {#key-concepts-and-use-cases}

### 常用辭彙表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **创意就绪资产：**&#x200B;已准备好与更广的团队共享的资产，或者已经由创意团队选择/批准与营销或 LOB 团队共享的资产。

* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。

* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本文档中，除非另有特别说明，否则它与 Experience Manager Assets 同义。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM 用户可以是营销或非营销用户，例如业务线 (LOB) 用户、管理员、销售人员等。

### 使用Experience Manager和Creative Cloud整合時的注意事項 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

這是Experience Manager和Creative Cloud整合的最佳實務的簡短摘要。 請閱讀本檔案的其餘部分，以取得這些內容的詳細瞭解。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括清晰處理從Experience Manager結帳的資產進行中工作
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：** 使用Experience Manager案頭應用程式
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 從Experience Manager Assets存取Adobe Stock資產 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) 讓Experience Manager使用者能夠從Adobe Stock搜尋、預覽、授權及儲存資產至Experience Manager。 授權並儲存的Adobe Stock資產已選取Stock中繼資料，可透過額外篩選器用來搜尋這些資產。

關於這項整合的一些要點：

* Adobe庫存中的資產儲存至Experience Manager後，會變成一般Experience Manager Assets，而二進位檔案會儲存至Experience Manager存放庫。 系統會為資產儲存Experience Manager中與Adobe Stock相關的一些中繼資料，否則擷取程式看起來會與任何其他檔案相同。 例如，如果智慧標籤處於作用中狀態，則會在儲存時將標籤新增至這些資產。
* 儲存至Experience Manager的資產為復本，而非返回Adobe Stock的連結。

**使用Creative Cloud中從Adobe Stock儲存至Experience Manager的資產**. 此整合獨立於Adobe Asset Link，但Adobe Asset Link可辨識以此方式從Stock儲存的這些資產，並在Photoshop、Illustrator或InDesign的Adobe Asset Link擴充功能UI中，在這些資產上顯示其他中繼資料和庫存圖示。 這些檔案可供瀏覽、開啟等操作，因為它們是儲存為Experience Manager時的一般Experience Manager資產。
使用具有Adobe Asset Link擴充功能之Creative Cloud應用程式的創意使用者，除了可以從Adobe Stock存取已獲得授權的Experience Manager資產外，也可以使用Creative Cloud資料庫面板來搜尋、預覽和授權Adobe Stock資產。
從Adobe Stock授權並儲存至Experience Manager的資產可供存取Experience Manager Assets部署的更廣泛團隊使用，而透過Creative Cloud資料庫面板從Adobe Stock授權資產的創意內容只能預設在其Creative Cloud帳戶中供他們自己使用。

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

若要在創意和行銷/業務線(LOB)團隊之間設計有效率的工作流程，並選擇最佳支援功能，請務必瞭解資產儲存在DAM的時機和原因。

### 為何資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓您輕鬆存取及找到資產。 它可確保組織或生態系統（包括合作夥伴、客戶等）的眾多使用者都能運用這些資產。

大部分組織會選擇僅儲存與下遊行銷/LOB程式相關的資產(透過Experience Manager Sites發佈至網路頻道等頻道，或由Adobe Experience Cloud提供的其他頻道(Marketing Cloud、Advertising Cloud和Analytics Cloud測量，提供給使用者/合作夥伴等)。 此外，組織會儲存資產，這些資產可能需經過DAM的稽核/核准程式。 如此一來，DAM主要儲存極有可能利用的資產，並避免儲存閒置資產。

儲存資產也受到技術和資源使用率的考量所限制。 DAM提供有關已儲存資產的其他服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考和新增存取控制資訊。 這些服務會消耗額外的時間和基礎建設資源。

通常，儲存所有資產和更新是不合需要的。 例如，如果特定資產的更新品質不佳並消耗過多資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對儲存資產生命週期每個階段的資產不感興趣。 例如，他們會避免在下列情況下儲存資產：

* 尚未完成或有待實驗的資產
* 未通過創意/內部團隊稽核週期的資產
* 相較於相關資產，團隊擁有更出色的候選人來向外部團隊代表其工作

通常，以下類別資產會儲存在DAM中：

* 達到特定到期日且視為可共用的資產
* 創意團隊預先選取的資產
* 行銷可用或要求的特定資產格式，視特定合約或協定而定(例如，從RAW檔案轉換的JPG檔案、來自PSD原始檔的TIFF/影像)

#### 當資產的更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，只有與更廣泛的DAM使用者集相關的資產更新才應儲存在DAM中。 這可確保使用者（行銷和類似功能）只能在DAM資產時間軸中看到相關版本。

通常會與資產生命週期中的主要里程碑相關的變更。 例如，初始行銷就緒資產或根據創意團隊提供的請求/稽核的正式更新應儲存在DAM中並進行版本設定。

在請求變更DAM中的現有資產後，創意團隊的更新以供行銷團隊檢閱，這是相關更新的範例。 它應儲存在DAM中並進行版本設定，以供進一步參考或回覆至先前的版本。

以下是通常無關的更新範例：

* 在資產準備好供行銷稽核之前上傳資產的早期版本
* 創意和行銷團隊決定資產準備好之前，經常在工作階段對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

根據使用者對Experience Manager Assets部署的存取權，Experience Manager Assets支援兩種型別的使用者。 通常企業網路（防火牆）內的使用者可以直接存取DAM。 企業網路以外的其他使用者無法直接存取。 使用者型別會從技術角度決定可使用哪些整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或加入內部網路的代理/創意專業人士有權存取DAM執行個體，包括Experience Manager登入。 Experience Manager和網路基礎架構可設定為允許直接存取外部合作對象（通常是受信任的組織，例如為客戶工作的機構），以透過網路（例如，透過VPN或IP允許清單）存取Experience Manager。

在這種情況下，Adobe資產連結或Experience Manager案頭應用程式可讓您輕鬆存取最終/核准的資產，並可將創意就緒的資產儲存至DAM。

#### 沒有DAM存取權的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM例項的外部機構和自由職業者可能會要求存取已核准的資產，或想要將其新設計新增到DAM。

使用下列策略提供最終/核准資產的存取權：

* 如果Asset Link無法運作，請使用案頭應用程式。
* 使用 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於將資產安全地分發給外部合作夥伴
* 根據以下專案使用自訂的發佈和sourcing入口網站實施： [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用Experience Manager中設定的存取控制和必要的網路基礎結構（例如VPN和IP允許清單），讓外部各方能夠存取DAM中的專用內容區域。 他們可以使用Experience Manager Web UI來取得資產，並將新內容上傳到您的DAM中。

#### 正在從Experience Manager處理資產 {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議對資產進行重大更新，有時稱為進行中的工作，而不需將所有編輯內容儲存至本機檔案，也不會以變更的形式上傳至Experience Manager。 這可加快案頭使用者的工作速度、限制使用的網路頻寬、保持資產時間表整潔並專注於受控制的重大更新。

Adobe Asset Link對此使用案例提供良好的支援：

* 當Photoshop、InDesign或Illustrator中的使用者想要編輯檔案時，會對指定的資產執行簽出操作
* 資產會於背景下載，並透過Creative Cloud案頭應用程式放入與磁碟同步的使用者Creative Cloud帳戶中，而簽出旗標則會切換為資產上的Experience Manager，以將編輯衝突減至最低
* 從此處，使用者可在檔案中工作，該檔案儲存在同步位置的本機中，並可繼續工作並按需要頻率儲存必要的變更
* 此外，由於資產位於Creative Cloud帳戶中，使用者可能擁有的其他裝置也可使用該資產(例如，可在專用的Creative Cloud行動應用程式中開啟或編輯資產)，並可與其他Creative Cloud使用者共用，以進行共同作業。
* 當創意使用者完成變更時，他們可以在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上可選註釋。 Experience Manager中對應的資產會建立版本，並使用新的二進位檔更新為。 行銷人員或LOB使用者等Experience Manager使用者可透過Experience Manager資產時間軸UI存取重大資產變更或里程碑。

Experience Manager案頭應用程式為在原生應用程式中開啟的資產提供網路共用。 依預設，本機完成的所有變更都會在短暫後自動上傳至Experience Manager。 透過這種設定，進行中階段期間的頻繁儲存都將上傳到Experience Manager並進行版本設定，造成大量網路流量和潛在的可擴充性挑戰，更不用說Experience Manager中的不必要版本了。

這裡建議的方法是使用Experience Manager案頭應用程式中的選項來關閉自動更新，並運用應用程式資產狀態UI中的上傳變更動作手動上傳資產變更以Experience Manager。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能會需要同時將大量檔案上傳到DAM中，例如：

* 上傳拍照或較大專案的結果
* 上傳創意公司提供的資產
* 如果選取是在DAM外部完成，則從較大的集合上傳選取的資產

請注意，本說明將檔案上傳作為案頭使用者工作流程的一般部分，以作業方式上傳（例如，每週或每次拍照）。 這裡不涵蓋大型資產移轉。

您可以善用下列上傳功能：

* 若要大量上傳大型/階層式資料夾，請使用提供下列功能的Experience Manager案頭應用程式 [資料夾上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) 功能。 您也可以上傳階層資料夾結構。 資產會於背景上傳，因此不會繫結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳一些檔案，請直接將檔案拖曳至網頁介面，或使用Experience Manager Assets網頁介面中的「建立」選項。
* 您也可以根據您的業務需求使用自訂上傳程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案共用」來管理數位資產，只需使用Experience Manager案頭應用程式對應的網路共用即可視為方便的替代方式。 從網路檔案共用轉換時，Experience Manager網頁介面提供了一組豐富的數位資產管理功能，遠遠超越了網路共用上的能力（搜尋、收集、中繼資料、共同作業、預覽等），而Experience Manager案頭應用程式則提供便利的連結，可將伺服器端DAM存放庫與案頭上的工作連結。

避免使用Experience Manager案頭應用程式直接在Experience Manager Assets的網路共用中管理資產。 例如，請避免使用Experience Manager案頭應用程式來移動/複製多個檔案。 請改用Experience Manager Assets網頁UI，將資料夾從Finder/Explorer拖曳至網路共用，或使用Experience Manager Assets資料夾上傳功能。

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
