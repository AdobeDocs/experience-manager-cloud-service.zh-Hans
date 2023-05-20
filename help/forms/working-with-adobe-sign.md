---
title: 使用方式 [!DNL Adobe Sign] 在最適化表單中？
description: 您可以啟用電子簽章([!DNL Adobe Sign])最適化表單的工作流程，可自動化簽署工作流程、簡化單一和多重簽名流程，並以電子方式簽署行動裝置的表單。
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 3d713304512065819ed16bbc9604f2cf9d1cf43f
workflow-type: tm+mt
source-wordcount: '3072'
ht-degree: 1%

---


# 使用 [!DNL Adobe Sign] 在最適化表單中 {#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] 支持自适应表单的电子签名工作流。電子簽章可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在一般情況下 [!DNL Adobe Sign] 最適化Forms情境中，使用者需填寫最適化表單來申請需要一或多個當事人簽名的服務。 例如，抵押貸款與信用卡申請需要所有借方與共同應徵者的合法簽名。 若要針對類似案例啟用電子簽章工作流程，您可以整合 [!DNL Adobe Sign] 最適化表單。 還有幾個範例是，您可以使用 [!DNL Adobe Sign] 至：

* 透過完全自動化的提案、報價和合約程式，完成任何裝置的交易。
* 更快完成人力資源流程，為員工提供數位體驗。
* 縮短合約週期時間，讓您的廠商更快上線。
* 建立自動化常見流程的數位工作流程。

[!DNL Adobe Sign] 與整合 [!DNL AEM Forms] 支援：

* 單一和多使用者簽署工作流程
* 循序和同步簽署工作流程
* 以匿名或登入使用者身分簽署表單
* 動態簽署程式（與整合） [!DNL AEM Forms] 工作流程)
* 透過知識庫、電話、社交設定檔和政府ID進行驗證
* 指派角色給每個協定收件者。 適用於商業和企業服務等級的Adobe Sign可選擇擴充 [協定收件者的角色](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## 前提条件 {#prerequisites}

使用前 [!DNL Adobe Sign] 在最適化表單中：

* 確定 [!DNL AEM Forms] as a Cloud Service已設定為使用Adobe Sign。 如需詳細資訊，請參閱 [將Adobe Sign與整合 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* 保持收件者清單準備就緒。 您至少需要每個收件者的電子郵件地址。

## 設定 [!DNL Adobe Sign] 最適化表單 {#configure-adobe-sign-for-an-adaptive-form}

進行設定 [!DNL Adobe Sign] 最適化表單：

1. [啟用 [!DNL Adobe Sign] 最適化表單](#enableadobsignforanadaptiveform)
1. [新增 [!DNL Adobe Sign] 最適化表單的欄位](#addadobesignfieldstoanadaptiveform)
1. [選取 [!DNL Adobe Sign] 最適化表單的Cloud Service](#select-adobe-sign-cloud-service-and-signing-order)

1. [新增 [!DNL Adobe Sign] 自適應表單的收件者](#addsignerstoanadaptiveform)
1. [為最適化表單選取提交動作](#selectsubmitactionforanadaptiveform)

![收件人详细信息](assets/signer_details_new.png)

### 啟用 [!DNL Adobe Sign] 最適化表單  {#enableadobesign}

您可以啟用 [!DNL Adobe Sign] 適用於現有的最適化表單或建立 [!DNL Adobe Sign] 啟用最適化表單。 選擇下列其中一項：

* [建立 [!DNL Adobe Sign] 啟用最適化表單](#create-an-adaptive-form-for-adobe-sign)
* [啟用 [!DNL Adobe Sign] 適用於現有的最適化表單](#editafsign).

#### 建立Adobe Sign適用性表單 {#create-an-adaptive-form-for-adobe-sign}

若要建立可啟用簽名的最適化表單：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**. 範本清單隨即顯示。 選取範本並點選 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 基本]** 標籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 最適化表單的預設值。

   1. 選取 [設定容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時間 [整合 [!DNL Adobe Sign] 替換為 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   設定容器包含 [!DNL Adobe Sign] 為您的環境設定的Cloud Services。 這些服務可在最適化表單編輯器中選取。

1. 在 **[!UICONTROL 表單模型]** 索引標籤中，選取下列其中一個選項：

   * 如果您有自訂表單範本，且需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 當您使用選項時，傳送供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 如果您沒有自訂表單範本，請選取 **[!UICONTROL 產生記錄檔案]** 選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 建立。]** 已建立可啟用簽名的最適化表單。 您可以新增 [!DNL Adobe Sign] 欄位放入表單並傳送以進行簽署。

#### 啟用 [!DNL Adobe Sign] 最適化表單 {#editafsign}

使用 [!DNL Adobe Sign] 在現有的最適化表單中：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 索引標籤中，選取 [設定容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 整合時建立 [!DNL Adobe Sign] 替換為 [!DNL AEM Forms].
1. 在 **[!UICONTROL 表單模式]** 索引標籤中，選取下列其中一個選項：

   * 如果您有自訂表單範本，且需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 當您使用選項時，傳送供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 如果您沒有自訂表單範本，請選取 **[!UICONTROL 產生記錄檔案]** 選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 儲存並關閉]**. 已針對以下專案啟用最適化表單 [!DNL Adobe Sign]. 現在，您可以新增 [!DNL Adobe Sign] 欄位放入表單並傳送以進行簽署。

### 新增 [!DNL Adobe Sign] 最適化表單的欄位 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 有多種欄位可放置在調適型表單上。 這些欄位接受各種型別的資料，例如簽名、縮寫、公司或標題，並協助在簽名期間收集額外的資訊以及簽名。 您可以使用 [!DNL Adobe Sign] 要置入的區塊元件 [!DNL Adobe Sign] 最適化表單中不同位置的欄位。

若要新增欄位至最適化表單，並自訂與這些欄位相關的各種選項：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器變更為最適化表單。 此 [!DNL Adobe Sign] 區塊元件具有所有支援的 [!DNL Adobe Sign] 欄位。 依預設，它會新增 **[!UICONTROL 簽章]** 最適化表單的欄位。

   ![簽署區塊](assets/sign_block_new.png)

   根據預設， [!DNL Adobe Sign] 封鎖在已發佈的最適化表單中不可見。 它只會顯示在簽署檔案中。 您可以變更下列專案的可見度 [!DNL Adobe Sign] 從的屬性封鎖 [!DNL Adobe Sign] 區塊元件。

   >[!NOTE]
   >
   >  * 使用 [!DNL Adobe Sign] 區塊並非強制使用 [!DNL Adobe Sign] 在最適化表單中。 如果您不使用 [!DNL Adobe Sign] 封鎖並新增收件者的欄位，則預設簽名欄位會顯示在簽署檔案的底部。
   >  * 使用 [!DNL Adobe Sign] 僅封鎖那些自動產生記錄檔案的最適化Forms。 如果您使用自訂XDP來產生記錄檔案或表單範本式的最適化表單， [!DNL Adobe Sign] 不支援此區塊。



1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 圖示。 它會顯示新增欄位和格式化欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全熒幕檢視

1. 點選 **[!UICONTROL Adobe Sign]** 欄位 ![Adobe Sign](assets/adobesign.png) 圖示。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 型別]** 下拉式欄位以選取 [!DNL Adobe Sign] 欄位並點選「完成」 ![儲存](assets/save_icon.svg) 圖示以將選取的欄位新增至 [!DNL Adobe Sign] 區塊。 此 **[!UICONTROL 型別]** 下拉式欄位包含簽名、收件者資訊和資料欄位型別。 [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 中列出的支援欄位 [!UICONTROL 型別] 下拉式方塊。 如需關於以下專案的詳細資訊： [!DNL Adobe Sign] 欄位，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選取必要選項，將欄位標示為必要欄位。 除了 **[!UICONTROL 名稱]** 和 **[!UICONTROL 必填]** 選項，部分 [!DNL Adobe Sign] 欄位有更多選項。 例如，遮色片和多行。 此外，請為每個欄位指定唯一的名稱 [!DNL Adobe Sign] 欄位是位於相同還是不同的欄位 [!DNL Adobe Sign] 個區塊。

   如果您選取 **[!UICONTROL 數位簽名]** 從下拉式清單中，您可以將數位簽名套用至最適化表單：

   * 使用雲端簽名透過進行線上簽署 [數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供者代管。
   * 透過Adobe Acrobat下載檔案，或使用智慧卡、USB代號或檔案式數位IDReader在本機。

### 啟用 [!DNL Adobe Sign] 最適化表單 {#enableadobsignforanadaptiveform}

開箱即用 [!DNL Adobe Sign] 未針對最適化表單啟用。 要启用该功能：

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/Smock_Wrench_18_N.svg) 圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。

### 選取 [!DNL Adobe Sign] Cloud Service和簽署順序 {#select-adobe-sign-cloud-service-and-signing-order}

您可以設定多個 [!DNL Adobe Sign] AEM執行個體的服務 [!DNL Forms]. 建議您為每個功能（人力資源、財務等）分別設定一組服務。 它可讓您更輕鬆追蹤及報告已簽署的檔案。 例如，一家銀行擁有多個部門。 您可以為每個部門設定個別的設定，以便更妥善地追蹤檔案。

一個檔案也可以有多個收件者。 例如，信用卡申請可以有多個應徵者。 在開始處理申請之前，銀行需要所有申請者的簽名。 對於多收件者情況，您可以選取以循序或同時順序簽署檔案。

若要選取Cloud Service和簽署順序，請執行下列動作：

![雲端服務](assets/cloud-service.png)

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/Smock_Wrench_18_N.svg) 圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。
1. 從已設定的清單中選取Cloud Service [!DNL Adobe Sign] Cloud Services。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 清單是空的，請遵循 [設定 [!DNL Adobe Sign] 替換為 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 設定服務的文章。

   下拉式清單會列出以下專案中存在的Cloud Services： `global` 「工具>中的資料夾」 **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 此外，下拉式清單也會列出您在所選資料夾中的Cloud Services **[!UICONTROL 設定容器]** 欄位建立最適化表單時。

1. 從中選擇簽署順序 **[!UICONTROL 收件者可以完成]** 對話方塊。 收件者可以簽署最適化表單 **[!UICONTROL 循序]**  — 一個接一個的收件者，或 **[!UICONTROL 同時]**  — 以任何順序。

   依照順序，一位收件者一次會收到Adobe Sign合約。 收件者完成指派的動作後，協定會傳送給下一個收件者，依此類推。

   所有收件者會以同時順序接收Adobe Sign合約，並可互相平行採取行動。

1. 使用「合約ID欄位」將繫結連結至合約ID (agreementId)。 它會新增協定ID至結構描述型表單之提交資料的afBoundData區段。 合約ID也會新增至所有啟用Adobe Sign之表單之提交資料中的afSubmissionInfo區段。 您可以使用協定ID來使用自訂程式碼追蹤協定狀態（需要自訂實施）。

1. [將收件者新增至最適化表單](working-with-adobe-sign.md#addsignerstoanadaptiveform) 然後點選「完成」 ![儲存](assets/save_icon.svg) 圖示以儲存變更。

### 將收件者新增至最適化表單 {#addsignerstoanadaptiveform}

Adobe Sign協定可以有一或多個收件者。 新增收件者時，您也可以設定收件者的驗證詳細資料，並選取表單填寫者與收件者是否為同一個人。 執行以下步驟，新增並提供收件者的各種詳細資訊：

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/Smock_Wrench_18_N.svg) 圖示。 它會開啟具有最適化表單容器屬性的屬性瀏覽器。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。
1. 點選 **[!UICONTROL 新增收件者]**. 它會新增收件者至最適化表單。 您可以將多位收件者新增至最適化表單。 所有收件者都會收到最適化表單提交作業的Adobe Sign合約。
   ![phone-details](assets/recipient-settings.png)

1. 按一下 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 圖示來指定下列關於收件者的資訊：

   * **[!UICONTROL 標題]：** 指定標題以唯一識別收件者。

   * **[!UICONTROL 收件人与填表人是否相同？]：** 選取 **[!UICONTROL 是]**，如果表單填寫者與第一個收件者是同一個人。 <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL 收件者角色]：** 選取收件者的角色。 適用於商業和企業服務等級的Adobe Sign可選擇擴充 [協定收件者的角色](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html)，超越 **簽署者**，以更符合其工作流程需求。

   * **[!UICONTROL 收件者電子郵件地址]：** 指定收件者的電子郵件地址。 收件者在指定的電子郵件地址上收到Adobe Sign合約。 您可以選擇使用表單欄位、登入使用者的Experience Manager使用者設定檔中提供的電子郵件地址，或手動輸入電子郵件地址。 此為必要步驟。

      >[!NOTE]
      >
      >確保第一個收件者或唯一收件者（如果有單一收件者）的電子郵件地址與 [!DNL Adobe Sign] 用來設定AEM Cloud Services的帳戶。

   * **[!UICONTROL 收件者驗證方法]：** 指定在開啟Adobe Sign合約之前驗證收件者的方法。 您可以在電話、知識庫、以社交身分為基礎的驗證和以下之間選擇： [政府ID](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html).
   >[!NOTE]
   >
   >    * 依預設，社交身分型驗證會提供使用Facebook、Google和LinkedIn驗證的選項。 您可以聯絡 [!DNL Adobe Sign] 支援啟用其他社交驗證服務提供者。


   * **[!DNL Adobe Sign]要填寫或簽署的欄位：** 選取 [!DNL Adobe Sign] 收件者的欄位。 一個最適化表單可以有多個 [!DNL Adobe Sign] 欄位。 您可以選擇為收件者啟用特定欄位。 欄位會顯示所有可用的 [!DNL Adobe Sign] 個區塊。 當您選取區塊時，會選取區塊的所有欄位。 您可以使用X圖示來取消選取欄位。

   ![recipient-details](assets/signer-details.png)

   上圖有兩個範例 [!DNL Adobe Sign] 區塊：個人資訊和辦公室詳細資訊

   點選 ![儲存](assets/save_icon.svg) 圖示。 收件者已新增。

### 為最適化表單選取提交動作 {#selectsubmitactionforanadaptiveform}

在您之後，新增 [!DNL Adobe Sign] 最適化表單的欄位，啟用 [!DNL Adobe Sign] 在表單容器中，選取 [!DNL Adobe Sign] Cloud Service並新增Adobe Sign協定收件者，請為最適化表單選取適當的提交動作。 如需最適化Forms提交動作的詳細資訊，請參閱 [設定提交動作](configuring-submit-actions.md).

簽署和提交表單彼此獨立。 使用者提交表單後，一旦建立Adobe Sign合約，最適化表單就會提交。 [!DNL AEM Forms] as a Cloud Service不會等待收件者簽署或完成其他動作以提交最適化表單。 使用者按一下「提交」按鈕或「摘要」步驟顯示表單摘要時，就會立即提交表單。

此外， [!DNL Adobe Sign] 啟用的最適化表單會內嵌Adobe Sign合約ID以提交資料。 您可以使用協定ID來使用自訂程式碼追蹤協定狀態（需要自訂實施）。

Adobe Sign合約ID (agreementId)包含在最適化表單的提交資料中。 依預設，合約ID會顯示在 `afSubmissionInfo` 已提交資料的節點。

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

您也可以選擇將繫結連結與協定ID (agreementId)建立關聯。 它會新增合約ID至已提交資料的afBoundData區段。 例如，在以下提交的資料中，合約ID會與 `<userName>` 節點：

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。 在已發佈的表單上， [!DNL Adobe Sign] 收件者收到透過電子郵件簽署的表單時，會顯示封鎖欄位。 當 **[!UICONTROL 收件者和填表人何時相同？]** 選項標示為「是」且符合條件，使用者在提交後會重新導向至Adobe Sign合約，且使用者可以立即簽署檔案，而非等待合約出現在電子郵件中。

## 設定最適化表單的雲端簽名 {#configure-cloud-signatures-for-an-adaptive-form}

雲端數位簽名或遠端簽名是新一代的數位簽名，可在案頭、行動裝置和Web上運作，並符合收件者驗證的最高合規性和保證標準。 您可以使用雲端數位簽名在最適化表格上簽名。

晚於 [編輯Adobe Sign的最適化表單屬性](working-with-adobe-sign.md#enableadobesign)，執行以下步驟以將雲端簽名欄位新增至最適化表單：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器變更為最適化表單。 此 [!UICONTROL Adobe Sign區塊] 元件具有所有支援的 [!DNL Adobe Sign] 欄位。 依預設，它會新增 **[!UICONTROL 簽章]** 最適化表單的欄位。

   ![簽署區塊](assets/sign-block-new.png)

1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 圖示。 它會顯示新增欄位和格式化欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全熒幕檢視

1. 點選 **[!UICONTROL Adobe Sign欄位]** ![Adobe Sign](assets/adobesign.png) 圖示。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 型別]** 要選取的下拉式欄位 **[!UICONTROL 數位簽名]** 然後點選 **[!UICONTROL 完成]** 圖示以將選取的欄位新增至 [!DNL Adobe Sign] 區塊。

   ![數位簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   使用以下將數位簽名套用至最適化表單：

   * 雲端簽名：使用 [數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供者代管。
   * Adobe Acrobat或Reader：使用Adobe Acrobat或Reader下載並開啟檔案，以使用智慧卡、USB權杖或檔案式數位ID簽名。

   將雲端簽名欄位新增至最適化表單後，執行以下步驟以完成設定程式：

   * [為最適化表單啟用Adobe Sign](#enableadobsignforanadaptiveform)
   * [為最適化表單選取Adobe Sign Cloud Service](#selectadobesigncloudserviceforanadaptiveform)
   * [將收件者新增至最適化表單](#addsignerstoanadaptiveform)
   * [為最適化表單選取提交動作](#selectsubmitactionforanadaptiveform)


### 設定感謝頁面或摘要步驟元件 {#configure-the-thank-you-page-or-summary-step-component}

此 **[!UICONTROL 摘要步驟]** 元件會自動提交表單、填入自訂摘要頁面內的資訊，並顯示已提交表單的摘要。 摘要步驟元件會佔據表單可用的完整寬度。 建議在包含摘要步驟元件的區段上不要有任何其他元件。

## 常见问题 {#frequently-asked-questions}

**問：** 您可以將最適化表單內嵌在其他最適化表單中。 內嵌的最適化表單可以是 [!DNL Adobe Sign] 已啟用？
**ans：** 否，Experience Manager Forms不支援使用內嵌 [!DNL Adobe Sign] 啟用最適化表單以供簽署

**問：** 使用進階範本建立調適型表單並開啟表單進行編輯時，出現「電子簽章或收件者設定不正確」的錯誤訊息。 出現。 如何解決錯誤訊息？
**ans：** 使用進階範本建立的最適化表單已設定為使用 [!DNL Adobe Sign]. 若要解決錯誤，請建立並選取 [!DNL Adobe Sign] 雲端設定和設定 [!DNL Adobe Sign] 最適化表單的收件者。

**問：** 我可以使用 [!DNL Adobe Sign] 最適化表單的靜態文字元件中的文字標籤？
**ans：** 可以，您可以在文字元件中使用文字標籤來新增 [!DNL Adobe Sign] 記錄檔案的欄位（僅限自動產生的記錄檔案選項）已啟用的最適化表單。 若要瞭解建立文字標籤的程式和規則，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/using/text-tag.html). 另請注意，最適化Forms對文字標籤的支援有限。 您只能使用文字標籤來建立符合以下條件的欄位： [Adobe Sign區塊](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支援。

## 疑难解答 {#troubleshoot}

### [!DNL Adobe Sign] 合約失敗 {#adobe-sign-agreement-failures}

**問題**
時間 [!DNL Adobe Sign] 已針對最適化表單設定服務，該服務無法建立 [!DNL Adobe Sign] 最適化表單的合約。

**解决方法**

* 檢查 [Adobe Sign Cloud Service的設定](adobe-sign-integration-adaptive-forms.md) 用於最適化表單中。
* 確定API應用程式位於 [!DNL Adobe Sign] 用於設定的伺服器 [!DNL Adobe Sign] Cloud Service有必要的許可權。
* 如果您使用多個 [!DNL Adobe Sign] Cloud Services，指向 **[!UICONTROL oAuth URL]** 所有服務中的相同專案 **[!UICONTROL Adobe Sign Shard]**.

* 使用個別的電子郵件地址進行設定 [!DNL Adobe Sign] 第一個或單一收件者的帳戶和。 第一個收件者或唯一收件者（如果有單一收件者）的電子郵件地址不可與 [!DNL Adobe Sign] 用來設定AEM Cloud Services的帳戶。

## 相关文章 {#related-articles}

* [整合 [!DNL Adobe Sign] 替換為 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [使用的最佳實務 [!DNL Adobe Sign] 搭配Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
