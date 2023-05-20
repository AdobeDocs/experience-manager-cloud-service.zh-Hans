---
title: 在AEM Sites頁面中新增或建立最適化表單（核心元件）
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: 您可以在AEM Sites頁面中使用最適化表單（核心元件）來填寫和提交表單，而無需離開AEM Sites頁面。
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 1d5641dd07cc68dade247fe30bb57663872e5560
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 2%

---

# 使用AEM Sites編輯器建立或新增最適化表單 {#add-an-adaptive-form-to-aem-sites-page}

您可以在AEM Sites頁面中順暢地撰寫或內嵌最適化Forms，讓您的使用者直接填寫並提交表單而不需離開Sites頁面。 它有助於使用者停留在網頁其他元素的上下文中，同時與表單互動。

您可以選擇下列其中一種方法，建立最適化表單或將其新增至AEM Sites頁面：

* **使用最適化Forms容器元件建立最適化表單**：此 [最適化表單容器](#af-container-component) 元件可讓您直接在AEM Sites編輯器中利用Adaptive Forms元件，建置數位註冊體驗。 這項整合讓想在AEM Sites頁面中建立和管理表單的AEM Sites作者獲得流暢的體驗。

* **新增現有的最適化表單**：此 [最適化Forms — 內嵌(v2)](#embed-existing-af) 元件可讓您輕鬆地將預先存在的最適化表單新增到AEM Sites中的頁面。 此功能增強最適化Forms的適應性和可重複使用性。 這項整合為客戶提供了便利的方式，可重複使用他們已建立的最適化Forms。

* **使用最適化Forms精靈建立表單**：使用 [最適化Forms — 內嵌(v2)](#embed-new-af) 元件以使用「表單建立精靈」從AEM Sites編輯器建立調適型表單。 表單會儲存為外部實體。 您也可以在其他Sites頁面和獨立表單中重複使用此表單。

* **在AEM Sites頁面中新增多個最適化Forms**：若要在AEM Sites頁面中新增多個最適化Forms，請使用AEM Forms容器元件 —  [最適化Forms — 內嵌(v2)](#embed-new-af) 和 [最適化表單容器](#af-container-component). 如果您需要在AEM Sites頁面中新增多個調適型表單作為div，則可以使用調適型表單容器元件。

您可以使用規則編輯器來新增或控制最適化表單元件的動態行為。 例如，隱藏或顯示元件。 規則編輯器不適用於非最適化表單元件。 因此，在AEM Forms Container元件中使用非最適化表單元件時，請務必謹慎。

## 使用最適化Forms容器元件建立最適化表單 {#af-container-component}

此 [!UICONTROL 最適化表單容器] 元件可讓您在AEM Sites編輯器中使用Adaptive Forms元件來建置數位註冊體驗。 您可以拖放表單元件，建立最適化表單。

### 前提条件 {#prerequisites-af-container}

+++ 啟用 **[!UICONTROL 最適化Forms容器]** 元件。

若要啟用 [!UICONTROL 最適化Forms容器] 元件執行範本原則中的下列步驟：

1. 前往 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯範本]
1. 按一下 [!UICONTROL 原則] 並選取 **[!UICONTROL 最適化Forms容器]**  核取方塊於 **[AEM原型專案名稱]  — 最適化表單**.
1. 按一下 **[!UICONTROL 完成]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ 在AEM Sites頁面中加入Adaptive Forms使用者端資料庫

若要在AEM Sites頁面中使用最適化Forms元件，請使用AEM Archetype/Git存放庫和部署管道，將Customheaderlibs和Customfooterlibs使用者端程式庫加入AEM Sites頁面。

1. 開啟您的 [AEM Forms原型或複製的Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 在文字編輯器中專案。 例如，Visual Studio Code。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製值 `sling:resourceSuperType`. 例如，值為 `core/wcm/components/page/v3/page`.

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似的結構 `ui.apps/src/main/content/jcr_root/apps` 與 `core/wcm/components/page/v3/page`.

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 新增 `customheaderlibs.html` 和 `customfooterlibs.html` 檔案。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   customfooterlibs.html用於JavaScript，而customheaderlibs.html用於css。

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署變更。

+++

### 使用最適化Forms容器元件建立最適化表單 {#create-af-using-af-container}


若要使用建立最適化表單 [!UICONTROL 最適化Forms容器] 元件：

1. 在編輯模式下開啟AEM Sites頁面。
1. 在元件瀏覽器面板中，拖放 **[!UICONTROL 最適化Forms容器]** 元件時。
1. 使用最適化Forms元件建立最適化表單。
1. 儲存設定。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

您的表單已準備就緒。 當您發佈AEM Sites頁面時，會自動發佈最適化表單及其相關參考資產。

#### 設定最適化表單容器屬性 {#configure-additional-settings-container}

您可以自訂 [!UICONTROL 最適化表單容器] 元件。 例如，

* 您可以設定預填服務在網站頁面上載入具有預填值的最適化表單。
* 您可以設定資料模型設定，以將最適化表單與資料來源建立關聯。
* 您可以設定提交動作，以便在提交表單時在Microsoft® OneDrive、Microsoft®OneDrive或其他資料來源上傳送資料。 您也可以為最適化Forms建立和選取自訂提交動作。

若要設定 **[!UICONTROL 最適化Forms容器]** 元件，按一下 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在動作列上。 此 **[!UICONTROL 編輯最適化Forms容器]** 對話方塊開啟。

![“编辑”对话框](/help/forms/assets/adaptiveformcontainer-editdialog.png)

在 [!UICONTROL 編輯最適化Forms容器] 對話方塊中，您可以指定下列專案。
* **“基本”选项卡**
   * **預填服務**：您可以使用預填服務，使用現有資料自動填入最適化表單的欄位。 當使用者開啟表單時，這些欄位的值會預先填充。 如需預填服務的詳細資訊，請參閱 [預填自適應表單欄位](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **使用者端資料庫類別**：指定 [JavaScript函式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 運算式中使用且受到Adaptive Forms支援的欄位。
* **資料模型**：資料模型可讓您將實體和服務從不同的資料來源整合到最適化表單中。 選擇 **[!UICONTROL 表單資料模型]** 如果您要建立的最適化表單涉及從多個資料來源擷取及寫入資料，請改為從多個資料來源擷取及寫入資料。
   * **表單資料模型**：表單資料模型可讓最適化表單與不同的資料來源通訊。 如需設定資料來源的詳細資訊，請參閱 [設定資料來源。](/help/forms/configure-data-sources.md)
   * **結構描述**：結構描述代表組織中後端系統產生或使用資料的結構。 您可以 [將結構描述關聯至最適化表單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) 並使用其元素將動態內容新增至最適化表單。

      >[!NOTE]
      >
      > 設定表單資料模型後，您無法變更關聯的表單模型。 不過，您可以修改與表單資料模型相關聯的結構描述。

* **“提交”选项卡**

   * **重定向到 URL**
      * **重新導向URL/路徑**：指定在提交後將最適化表單重新導向到的URL或路徑。

      * **提交動作**：當使用者按一下最適化表單上的提交按鈕時，會觸發提交動作。 您可以 [在最適化表單上設定提交動作](/help/forms/configuring-submit-actions.md). 調適型表單提供下列立即可用的提交動作：
         * 提交至REST端點
         * 发送电子邮件
         * 使用表单数据模型提交
         * 叫用AEM工作流程
         * 提交到 SharePoint
         * 提交到 OneDrive
         * 提交到 Azure Blob Storage

   您也可以 [擴充預設提交動作](custom-submit-action-form.md) 以建立您自己的自訂提交動作。

* **显示消息**
   * **訊息內容**：使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有當您選擇顯示感謝訊息時，才可使用此選項。

## 內嵌最適化表單  {#aem-container-component}

使用 **[!UICONTROL 最適化Forms — 內嵌(V2)]** 元件，您可在網站頁面中內嵌新的最適化表單或內嵌現有的最適化表單。 此 [!UICONTROL 最適化Forms — 內嵌(v2)] 元件可讓您：

* [新增現有的最適化表單](#embed-new-af)

* [建立和新增最適化表單](#embed-existing-af)

### 前提条件 {#prerequisites}

+++ 啟用 **最適化Forms — 內嵌** 元件。

若要啟用 [!UICONTROL 最適化Forms — 內嵌(v2)] 元件執行範本原則中的下列步驟：

1. 前往 [!UICONTROL 頁面資訊] > [!UICONTROL 編輯範本]

1. 按一下 [!UICONTROL 原則] 並選取 **[!UICONTROL 最適化表單 — 內嵌(v2)]** 核取方塊於 **[!UICONTROL [AEM原型專案名稱] - FORMS]** 群組。
1. 按一下 **[!UICONTROL 完成]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ 在AEM Sites頁面中加入Adaptive Forms使用者端資料庫

當 **[!UICONTROL 當表單涵蓋頁面的整個寬度時]** 選項已選取 **[!UICONTROL 表單容器]** 設定對話方塊和 **使用核心元件的最適化Forms** 都會使用，因此必須在您對應的網站頁面上包含clientlibs。

![覆蓋Gif](/help/forms/assets/overlaycorecomponent.gif)

若要在AEM Sites頁面中使用最適化Forms元件，請包含 `Customheaderlibs` 和 `Customfooterlibs` 使用AEM Archetype/Git存放庫和部署管道將使用者端程式庫移至AEM Sites頁面。

1. 開啟您的 [AEM Forms原型或複製的Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 在文字編輯器中專案。 例如，Visual Studio Code。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 複製值 `sling:resourceSuperType`. 例如，值為 `core/wcm/components/page/v3/page`.

   ![sling資源](/help/forms/assets/slingresource.png)

1. 在位置建立類似的結構 `ui.apps/src/main/content/jcr_root/apps` 與 `core/wcm/components/page/v3/page`.

   ![覆蓋結構](/help/forms/assets/overlaystructure.png)

1. 新增 `customheaderlibs.html` 和 `customfooterlibs.html` 檔案。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   此 `customfooterlibs.html` 用於JavaScript和 `customheaderlibs.html` 用於CSS。

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署變更。

+++

### 新增現有的最適化表單至AEM Sites頁面 {#embed-existing-af}

1. 在編輯模式下開啟AEM Sites頁面。
1. 在元件瀏覽器面板中，拖放 [!UICONTROL 最適化Forms — 內嵌] 元件時。
1. 點選 [!UICONTROL 最適化Forms — 內嵌] 元件於「網站」頁面並點選 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在動作列上。 此 **[!UICONTROL 編輯最適化Forms — 內嵌]** 對話方塊開啟。
1. 瀏覽並選取最適化表單，以內嵌於 [!UICONTROL 資產路徑].
1. 儲存設定。 最適化表單現在內嵌在頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### 建立最適化表單並新增至AEM Sites頁面 {#embed-new-af}

1. 在編輯模式下開啟AEM Sites頁面。
1. 在元件瀏覽器面板中，拖放 [!UICONTROL 最適化Forms — 內嵌(v2)] 元件時。
1. 按一下 **加號** 圖示後，您就會被重新導向至表單建立精靈。

   ![最適化Forms — 內嵌元件](/help/forms/assets/aemformcontainer.png)

1. 從建立新的最適化表單 [!UICONTROL 表單建立] 精靈。
1. 此 [!UICONTROL 資產路徑] 已包含已建立的最適化表單的路徑
1. 儲存設定。 最適化表單現在內嵌在頁面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### 設定最適化表單 — 內嵌(v2)屬性 {#configure-adaptive-form-embed}

您可以自訂 [!UICONTROL 最適化表單 — 內嵌(v2)] 元件。 在 [!UICONTROL 編輯最適化Forms — 內嵌(v2)] 對話方塊中，您可以指定下列專案。

* **資產路徑**：瀏覽並選取要內嵌的最適化表單。 如果您從「資產」瀏覽器中將其刪除，則會自動填入。
* **貼文提交** ：選取要在表單提交時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。
   * **顯示感謝訊息**：使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有當您選擇顯示感謝訊息時，才可使用此選項。
   * **顯示感謝頁面**：瀏覽並選取表單提交時顯示的頁面。 只有當您選擇顯示感謝頁面時，才可使用此選項。
   * **重新導向至感謝頁面**：啟用選項，將包含內嵌最適化表單的頁面取代為感謝頁面。 否則，「感謝您」頁面會取代以下位置的最適化表單： [!UICONTROL 最適化Forms — 內嵌] 元件，而不需重新整理頁面上的基礎網站。 只有當您選擇顯示感謝頁面時，才可使用此選項。
* **使用頁面語言**：使用AEM Sites頁面的本機，而非最適化表單的地區設定。
* **設定表單焦點**：選取以將焦點設定在最適化表單的第一個欄位上。
* **表單覆蓋框架的整個寬度**：如果勾選，iFrame將不會用於演算表單。
* **高度**：指定容器的高度。 保留空白以自動調整容器大小。
* **CSS使用者端資源庫**：指定CSS使用者端資料庫的路徑。

### 發佈已新增使用最適化表單的最適化Forms — 內嵌(v2)元件  {#publish-embedded-adaptive-form}

考慮以下情境來使用發佈新增的最適化Forms **[!UICONTROL 最適化表單 — 內嵌(v2)]** 元件：

* 第一次發佈AEM Sites頁面時，會自動發佈新增至Sites頁面的表單。
* 修改新增至已發佈Sites頁面的最適化表單時，請手動發佈對應的最適化Forms。
* 當您修改Sites頁面和對應的調適型Forms時，請重新發佈Sites頁面和新增到Sites頁面的所有調適型Forms。

### 使用最適化表單 — 內嵌(v2)元件修改新增的最適化Forms  {#modifying-embedded-adaptive-form}

若要修改最適化表單的任何設定或屬性，請執行下列任一項作業：

* 在個別編輯器中以最適化表單開啟原始表單，並加以修改。
* 在編輯模式下，從網站頁面內點選「最適化表單」，然後點選 **[!UICONTROL 在新視窗中編輯]**. 原始表單會以您可以修改的編輯模式開啟。

## 變更新增至AEM Sites頁面的最適化表單版面 {#change-layout-af-aem-sites-page}

在AEM Sites頁面中， [版面模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) 可讓您調整已建立或新增至AEM Sites頁面的最適化表單大小。

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM網站頁面會維護最適化表單的參考。 當您翻譯AEM Sites頁面時，該頁面會使用 [翻譯專案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) 翻譯成其他語言。

## 最佳實務 {#best-practices}

* 內嵌表單中不包含原始表單的頁首和頁尾。
* 使用者草稿和嵌入式表單的提交受到支援，並可在Forms Portal的草稿和已提交的Forms標籤中看到。