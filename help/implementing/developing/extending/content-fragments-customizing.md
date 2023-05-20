---
title: 自定义和扩展内容片段
description: 內容片段可擴充標準資產。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager as a Cloud Service中，內容片段可擴充標準資產；請參閱：

* [建立和管理內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) 和 [使用內容片段編寫頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md) 以取得有關內容片段的進一步資訊。

* [管理資產](/help/assets/manage-digital-assets.md) 以取得標準資產的詳細資訊。

## 架构 {#architecture}

基本 [組成部分](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的內容片段包括：

* A *內容片段*，
* 由一或多個 *內容元素*，
* 而且可以有一或多個 *內容變數*.

個別內容片段是根據內容片段模型：

* 內容片段模型會在建立內容片段時定義其結構。
* 片段會參考模型；因此對模型的變更可能會/將會影響任何相依片段。
* 模型是資料型別的建置模型。
* 新增新變數的函式等必須相應地更新片段。

   >[!NOTE]
   >
   >若要顯示/轉譯內容片段，您的帳戶必須具備 `read` 模型的許可權。

   >[!CAUTION]
   >
   >對現有內容片段模式所做的任何變更都可能影響相依片段，都可能導致這些片段中出現孤立屬性。

### Sites與資產的整合 {#integration-of-sites-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 內容片段為資產。
* 他們使用現有的Assets功能。
* 它們與Assets （管理主控台等）完全整合。

內容片段可視為網站功能，如下所示：

* 它們會在編寫頁面時使用。

#### 將內容片段對應至資產 {#mapping-content-fragments-to-assets}

![將內容片段移至資產](assets/content-fragment-to-assets.png)

根據內容片段模型的內容片段會對應至單一資產：

* 所有內容都儲存在 `jcr:content/data` 資產節點：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數會儲存在具有變數名稱的子節點下：例如， `jcr:content/data/myvariation`

   * 每個元素的資料都會儲存在個別子節點中，作為具有元素名稱的屬性：例如element的內容 `text` 儲存為屬性 `text` 於 `jcr:content/data/master`

* 中繼資料和相關內容儲存在下方 `jcr:content/metadata`
除了標題和說明之外，這些不會視為傳統中繼資料並儲存在 
`jcr:content`

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於下方：

`/content/dam`

#### 資產許可權 {#asset-permissions}

如需詳細資訊，請參閱 [內容片段 — 刪除考量事項](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### 功能整合 {#feature-integration}

若要與資產核心整合：

* 內容片段管理(CFM)功能以Assets核心為基礎。

* CFM針對卡片/欄/清單檢視中的專案提供自己的實作；這些外掛程式會插入現有的Assets內容演算實作中。

* 已擴充多個Assets元件，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [內容片段元件是核心元件的一部分](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans). 另請參閱 [開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) 以取得更多詳細資料。

內容片段可以從AEM頁面參照，就像任何其他資產型別一樣。 AEM提供 **[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)** - a [可讓您在頁面上包含內容片段的元件](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). 您也可以擴充此功能 **[內容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** 核心元件。

* 元件使用 `fragmentPath` 屬性以參考實際內容片段。 此 `fragmentPath` 屬性的處理方式與其他資產型別的類似屬性相同；例如，當內容片段移動到另一個位置時。

* 元件可讓您選取要顯示的變數。

* 此外，可以選取段落範圍來限制輸出；例如，這可用於多欄輸出。

* 元件允許中間內容：

   * 元件可讓您在此處放置其他資產（影像等） 位於參考片段的段落之間。

   * 對於中間內容，您需要：

      * 請注意不穩定參考的可能性；中間內容（製作頁面時新增）與其旁邊段落沒有固定的關係，在中間內容位置前插入新段落（在內容片段編輯器中）可能會失去相對位置

      * 請考慮使用其他引數（例如變異和段落篩選器）來設定要在頁面上呈現的內容

>[!NOTE]
>
>**内容片段模型:**
>
>在頁面上使用內容片段時，會參考它所根據的內容片段模式。
>
>這表示如果您在發佈頁面時尚未發佈模型，系統會標籤此模型，並將模型新增至要與頁面一起發佈的資源。

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可以與：

* **翻譯**

   內容片段已完全與整合 [AEM翻譯工作流程](/help/sites-cloud/administering/translation/overview.md). 在架構層級，這表示：

   * 內容片段的個別翻譯實際上是個別的片段；例如：

      * 它們位於不同的語言根下；但在相關語言根下共用完全相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了規則型路徑以外，內容片段的不同語言版本之間沒有進一步的連線；這些版本會作為兩個獨立的片段處理，雖然UI提供了在語言變體之間導覽的方法。
   >[!NOTE]
   >
   >AEM翻譯工作流程適用於 `/content`：
   >
   >* 由於內容片段模型存放在 `/conf`，這些不會包含在這類翻譯中。 您可以國際化UI字串。


* **元数据架构**

   * 內容片段（重新）使用 [中繼資料結構](/help/assets/metadata-schemas.md)，可使用標準資產定義。

   * CFM提供專屬的特定結構描述：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 個別結構表單已與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而非直接存取內容結構。

### 重要介面 {#key-interfaces}

下列三個介面可作為入口點：

* **內容片段** ([內容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   介面可讓您執行下列動作：

   * 管理基本資料（例如，取得名稱、取得/設定標題/說明）
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素(請參閱 [注意事項](#caveats))

      * 存取元素資料(請參閱 `ContentElement`)
   * 為片段定義的清單變數
   * 建立全域的新變數
   * 管理關聯內容：

      * 清單集合
      * 新增集合
      * 移除集合
   * 存取片段的模型

   代表片段主要元素的介面包括：

   * **內容元素** ([內容元素](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 存取元素的變數：

         * 清單變數
         * 依名稱取得變數
         * 建立新的變數(請參閱 [注意事項](#caveats))
         * 移除變數(請參閱 [注意事項](#caveats))
         * 存取變數資料(請參閱 `ContentVariation`)
      * 解決變異的捷徑（如果指定的變異不適用於某個元素，則套用一些其他實作特有的遞補邏輯）
   * **內容變數** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 根據上次修改資訊的簡單同步處理

   所有三個介面( `ContentFragment`， `ContentElement`， `ContentVariation`)擴充 `Versionable` 介面，新增內容片段所需的版本設定功能：

   * 建立元素的新版本
   * 列出元素的版本
   * 取得版本化元素的特定版本內容







### 調整 — 使用adaptTo() {#adapting-using-adaptto}

可調整以下內容：

* `ContentFragment` 可調整為：

   * `Resource`  — 基礎Sling資源；更新基礎 `Resource` 直接需要重建 `ContentFragment` 物件。

   * `Asset` - DAM `Asset` 代表內容片段的抽象；更新 `Asset` 直接需要重建 `ContentFragment` 物件。

* `ContentElement` 可調整為：

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html)  — 用於存取元素的結構資訊。

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` 可調整為：

   * `ContentFragment`

### 注意事项 {#caveats}

請注意：

* 整個API的設計目的是 **not** 自動保留變更（除非API JavaDoc另有說明）。 因此，您必須一律認可個別要求的資源解析器（或您實際使用的解析器）。

* 可能需要額外努力的任務：

   * 強烈建議從以下位置建立新的變數： `ContentFragment`. 這可確保所有元素都會共用此變數，並視需要更新適當的全域資料結構，以反映內容結構中新建立的變數。

   * 透過元素移除現有變數，使用 `ContentElement.removeVariation()`，不會更新指派給變數的全域資料結構。 若要確保這些資料結構保持同步，請使用 `ContentFragment.removeVariation()` 而是會從全域移除變數。

## 內容片段管理API — 使用者端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>使用者端API是內部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   此 `filter.xml` 用於內容片段管理的設定使其不會與資產核心內容套件重疊。

## 編輯工作階段 {#edit-sessions}

>[!CAUTION]
>
>請考慮此背景資訊。 您不應在此變更任何專案(因為它已標示為 *私人區域* 存放庫中)，但在某些情況下可能有助於瞭解事情在幕後如何運作。

編輯內容片段(可跨越多個檢視(=HTML頁面))是原子性的。 因此，原子多檢視編輯功能不是典型的AEM概念，內容片段使用所謂的 *編輯工作階段*.

當使用者在編輯器中開啟內容片段時，會啟動編輯工作階段。 當使用者透過選擇以下任一專案離開編輯器時，編輯工作階段即完成 **儲存** 或 **取消**.

技術上，所有編輯均於下列日期完成： *live* 內容，就像所有其他AEM編輯一樣。 開始編輯工作階段時，會建立目前未編輯狀態的版本。 如果使用者取消編輯，則會還原該版本。 如果使用者點按 **儲存**，不會執行任何特定動作，因為所有編輯作業都會在 *live* 因此，所有變更都會持續存在。 此外，按一下 **儲存** 將會觸發一些背景處理（例如建立全文檢索搜尋資訊及/或處理混合媒體資產）。

對於邊緣案例有一些安全措施；例如，如果使用者嘗試離開編輯器而未儲存或取消編輯工作階段。 此外，您也可以定期自動儲存，以防止資料遺失。
請注意，兩名使用者可能同時編輯相同的內容片段，因此可能會覆寫彼此的變更。 若要防止此情況，需要透過套用DAM管理的 *簽出* 對片段執行的動作。

## 示例 {#examples}

### 範例：存取現有的內容片段 {#example-accessing-an-existing-content-fragment}

若要達到此目的，您可以將代表API的資源調整為：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 範例：建立新內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立新的內容片段，您需要使用
`FragmentTemplate` 改編自模型資源。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

此 [自動儲存間隔](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) （以秒為單位測量）可使用設定管理員(ConfMgr)定義：

* 節點： `<conf-root>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 預設： `600` （10分鐘）；此值的定義日期為 `/libs/settings/dam/cfm/jcr:content`

如果您想要將自動儲存間隔設為5分鐘，您必須在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值： `300` （5分鐘等於300秒）

## 用於頁面編寫的元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) （建議）
