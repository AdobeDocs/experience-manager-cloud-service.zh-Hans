---
title: 如何建立最適化表單範本？
description: 使用範本編輯器建立最適化表單範本，以定義基本結構和初始內容。
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: c101ed97388b06dc71edfc9e13fac8a3e889c249
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 1%

---

# 建立最適化表單範本 {#adaptive-form-templates}

當您編寫表單時，可在編輯器中新增欄位和元件以定義表單結構、內容和動作。 您可以在「 」中新增欄位和元件 `guideRootPanel` 表單容器的。 使用範本編輯器，您可以建立包含作者可用來建立表單的基本結構和初始內容的範本。

例如，您希望所有表單作者在登錄檔單中都擁有某些文字方塊、導覽按鈕和提交按鈕。 您可以使用作者可用來建立與其他登錄檔單一致的表單的元件，來建立範本。 作者使用範本建立最適化表單時，新表單會繼承您在範本中指定的結構和元件。 範本編輯器可讓您：

* 在結構層中新增表單的頁首與頁尾元件。
* 提供表單的初始內容。
* 指定主題「提交動作」。

您可以下載並安裝 [!DNL AEM Forms] 引用內容包來自 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站，將參考主題和範本匯入您的環境。

## 使用範本 {#working-with-templates}

您可以導覽至「 」，從「工具」選單存取範本編輯器 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**. 在此處，範本會整理在啟用可編輯範本的資料夾中。

Experience Manager提供用來組織範本的全域資料夾。 不過，預設不會啟用。 您可以要求管理員啟用全域資料夾或建立範本資料夾。 如需如何建立資料夾的詳細資訊，請參閱 [範本資料夾](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### 创建模板 {#create-template}

建立資料夾後，請開啟資料夾，然後執行下列步驟來建立範本：

1. 點選 **[!UICONTROL 建立]** 在您建立的資料夾內。
1. 在「挑選範本型別」區段中，選取 **[!UICONTROL 自適應表單範本]** 並點選 **[!UICONTROL 下一個]**.

1. 在「範本詳細資訊」區段中，提供範本標題並點選 **[!UICONTROL 建立]**.
您也可以提供說明。

1. 點選 **[!UICONTROL 完成]** 以返回主控台，或點選 **[!UICONTROL 開啟]** 以在編輯器中開啟範本。

### 範本編輯器UI {#template-editor-ui}

開啟範本進行編輯時，您可以看到下列AEM Editor元件：

* **頁面工具列**
包含下列選項：

   * **切換側面板**：可讓您顯示或隱藏側欄。
   * **頁面資訊**：可讓您指定發佈/取消發佈時間、縮圖、使用者端資料庫、頁面原則和頁面設計使用者端資料庫等資訊。
      <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **模式選擇器：** 可讓您變更模式。您可以選擇 **[!UICONTROL 結構]** 模式， **[!UICONTROL 初始內容]**， **[!UICONTROL 版面配置控制]** 模式。 「結構」模式可讓您新增及自訂頁首與頁尾。 初始內容模式可讓您自訂表單內容。
   * **預覽：** 可讓您預覽範本在發佈時的外觀。 您可以使用「圖層選取器」和「預覽」來切換編輯和預覽模式。
* **側欄：** 提供內容、屬性、資產和元件瀏覽器。
* **元件工具列：** 選取元件時，您會看到可讓您自訂元件的工具列。
* **頁面**：新增內容以建立範本的區域。

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### 編輯範本 {#editing-a-template}

最適化表單範本是使用兩層來建立：

* 结构
* 初始内容

圖層選取器位於熒幕右上角的「預覽」選項旁。

### 结构 {#structure}

在範本編輯器中選取結構圖層時，您可以看到最適化表單容器上方和下方的版面容器。 作者可以將這些配置容器用於頁首和頁尾。 您可以新增、編輯或自訂頁首與頁尾。 將調適型表單標題元件拖放至版面容器中的調適型表單容器上方，以自訂範本標題。 將調適型表單頁尾元件拖放至版面容器中的調適型表單容器下方，以自訂範本頁尾。

![結構圖層中的版面配置容器](assets/header-layer-selector.png)

在結構圖層中配置容器

**答：** 頁首元件的佈局容器 **B.** 頁尾元件的配置容器

將版面容器中的最適化表單標題元件拖放到最適化表單容器上方。 新增元件後，您可以指定其屬性，讓您新增標誌並提供其標題。

同樣地，將頁尾元件拖放至最適化表單容器下方的版面容器時，可以提供版權資訊和公司詳細資訊。

![在「結構」圖層新增頁首與頁尾](assets/header-and-footer.png)

在「結構」圖層新增頁首與頁尾

#### 鎖定/解除鎖定結構層中的元件 {#locking-unlocking-components-in-the-structure-layer}

當您在選取了結構圖層的情況下編輯範本時，可以解鎖範本的頁首和頁尾。 如果範本中的元件已解除鎖定，表單作者可以在使用該範本的最適化表單中編輯元件。 鎖定元件會使表單作者無法在最適化表單中編輯該元件。 元件工具列中有鎖定選項。

例如，在範本中新增標題元件。 選取元件時，您會在元件工具列中看到鎖定選項。 通常頁首包含公司名稱和標誌，您不希望表單作者變更範本中的標誌和頁首。 在使用範本建立的最適化表單中，標題元件已鎖定，表單作者無法變更標誌和公司名稱。

>[!NOTE]
>
>不建議個別鎖定或解除鎖定頁首元件中的影像或標誌。 您可以解鎖標頭元件。

### 初始内容 {#initial-content}

選取「初始內容」選項時，範本的「最適化表單」容器會像要編輯的最適化表單一樣開啟。 如同製作最適化表單，您可以指定初始設定，例如選取主題和提交動作。

表單作者可將其用作建立表單的基礎。 內容流程結構會在範本的「初始內容」層指定。 若要切換到編輯表單範本的初始內容，在頁面工具列中的「預覽」之前，點選 ![畫佈下拉式清單](assets/canvas-drop-down.png) **>** **[!UICONTROL 初始內容]**.


在初始內容層中，您會建立作者用作基礎的最適化表單範本。 製作範本類似於製作表單，您會使用側邊欄中的可用選項。 側欄提供內容、屬性、資產和元件瀏覽器。

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>當您選取「儲存內容」或「儲存PDF」作為「提交動作」時，您會看到一個可指定「儲存」路徑的選項。 如果您在範本中指定路徑，則根據該範本建立的所有表單都會有相同的路徑。 您可以指定正確的儲存路徑，或確保表單作者更新路徑，以防止每個表單中的資料儲存於相同位置。

#### 建立具有索引標籤和面板的最適化表單範本 {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

例如，您想要建立具有下列標籤的範本：

* 常规信息
* 專業資訊

您已新增標誌、提供標題，並在結構圖層中新增頁尾。 鎖定頁首和頁尾，以防止表單作者在使用範本建立表單時編輯它們。

將圖層從「結構」變更為「初始內容」，並開始將內容新增至表單。 若要建立索引標籤結構，請在「最適化表單」容器的guideRootPanel中新增子面板。 若要新增面板：

* 您可以點選「 」 **[!UICONTROL +]** 按鈕(當您選取 **[!UICONTROL 將元件拖曳到這裡]** 選項。

* 您可以從側欄中的元件瀏覽器拖放面板元件。
* 您可以新增的子面板 `guideRootPanel` 元件工具列中的。

若要建立「一般資訊」和「專業資訊」標籤，請在 `guideRootPanel`. 選取面板並點選 ![cmppr](assets/configure-icon.svg) 以開啟側邊欄中的屬性。 將元素名稱變更為 `general-info` 和 `professional-info`和標題分別作為「一般資訊」和「專業資訊」。 在側邊欄中，點選內容以開啟內容瀏覽器。 在「表單物件」標籤中，選取 `guideRootPanel`. 在編輯器中，選取guideRootPanel。 點選 ![cmppr](assets/configure-icon.svg) 以開啟其屬性。 在「面板配置」欄位中，選取 **[!UICONTROL 索引標籤在頂端]** 並點選 **[!UICONTROL 完成]**. 標籤式範本結構即會套用。

#### 在索引標籤中新增內容 {#adding-content-in-tabs}

新增面板並將其建構為標籤後，您可以在標籤內新增欄位。 在編輯器中選取索引標籤時，您可以看到 **[!UICONTROL 將元件拖曳到這裡]** 選項。 您可以拖放元件，例如文字方塊、清單專案和按鈕。 您可以從側欄中的元件瀏覽器拖放元件。

每個元件都有可增強資料擷取和操控的屬性。 例如，您可以啟用 **[!UICONTROL 必要欄位]** 元件的屬性。 您的作者可以指定客戶在略過填寫必填欄位時看到的訊息。 在中指定訊息 **[!UICONTROL 必要欄位訊息]** 屬性。

在範例範本中，「一般資訊」索引標籤中會新增「名稱」、「電話號碼」和「出生日期」欄位。 在「專業資訊」標籤中，新增「目前僱用」、「僱用型別」、「教育資格」欄位。

新增欄位後，您可以新增「提交」和「重設」等按鈕。

### 啟用範本 {#enabling-the-template}

當您建立範本時，它會新增為草稿。 啟用範本以使用它來建立最適化Forms。 若要啟用範本：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 範本]**，然後開啟您建立範本的資料夾。

1. 您建立的範本會標示為「草稿」。
1. 選取範本並點選 **[!UICONTROL 啟用]** （在工具列中）。
建立最適化表單時，系統要求您選擇範本時，您會看到範本列出。

## 匯入或匯出範本 {#importing-or-exporting-a-template}

表單可與其範本搭配使用。 下載使用自訂範本建立的最適化表單時，範本未下載。 當您匯入其他表單時 [!DNL AEM Forms] 例如，會匯入而不包含範本。 如果表單已匯入，但其範本無法使用，則不會轉譯表單。 您可以封裝自訂範本，從 `/conf` 中的節點 `https://<server>:<port>/crx/packmgr`，並將其連線至 [!DNL AEM Forms] 您要上傳表單的執行個體。 您也可以 [使用AEM Archype建立範本並將其部署至您的Cloud Services執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * 您也可以設定 [!UICONTROL 記錄檔案] 直接從最適化表單編輯器或最適化表單範本編輯器存取範本。 如需詳細資訊，請參閱 [產生最適化Forms的記錄檔案](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).



## 建立表單資料模型結構描述與範本的關聯 {#associating-form-data-model-schema-in-template}

作者可以關聯 [!UICONTROL 表單資料模型結構描述] 至範本編輯器中的調適型表單範本。 它可讓作者從範本編輯器選取結構描述。 當您將結構描述與範本建立關聯，且表單作者根據範本建立表單時，系統會為表單預先選取結構描述。 它有助於表單作者規範結構描述的使用，並節省表單作者的時間。 若要在範本編輯器中選取表單資料模型結構描述：

1. 點選 **[!UICONTROL 內容瀏覽器]** 位於左側。
1. 前往表單容器 **[!UICONTROL 設定]**.
1. 選取 **[!UICONTROL 資料模型]**.
1. 選擇您的表單資料模型，透過 **[!UICONTROL 選取表單資料模型]** 並儲存設定。

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img.png)



## 使用範本建立最適化表單 {#creating-an-adaptive-form-using-the-template}

建立並啟用範本後，當您建立最適化表單時，可在表單管理員中使用範本。 若要使用範本並建立調適型表單，請參閱 [建立最適化表單](creating-adaptive-form.md).


<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, in order to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. -->

## 將最適化表單另存為範本 {#saving-adaptive-form-as-template}

您也可以將最適化表單儲存為範本，以供日後使用。 將最適化表單另存為範本：

1. 選取最適化表單以儲存為範本。
1. 按一下 **[!UICONTROL 另存為範本]**. 将显示一个对话框。
1. 指定 **[!UICONTROL 標題]** （必要欄位）， **[!UICONTROL 位置]** （必填欄位）和 **[!UICONTROL 說明]** （選擇性欄位）。
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![另存為表單為範本](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>若要使用與來源調適型表單相同的容器原則，建議將範本儲存在與來源調適型表單相同的資料夾中。 如果範本儲存在任何其他資料夾中，則建立的範本不會使用預設容器原則。

## 推荐 {#recommendations}

* 在範本編輯器中修改表單的屬性時，請勿使用BindReference屬性。
* 如果您想要新增中斷點，請在編寫最適化表單範本時建立中斷點。
如需中斷點的詳細資訊，請參閱 [回應式佈局](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
