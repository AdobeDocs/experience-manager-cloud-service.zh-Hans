---
title: 页面模板
description: 建立頁面時，會使用頁面範本作為新頁面的基礎
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: f5aa9229ff06fdcff5474594269ebcf9daf09e41
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 5%

---

# 页面模板 {#page-templates}

建立頁面時，您需要選取範本。 頁面範本會用作新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容以及可以使用的元件（設計屬性）。 這有幾個優點：

* 頁面範本可讓專業作者執行以下作業 [建立和編輯範本](/help/sites-cloud/authoring/features/templates.md).
   * 這類專業作者稱為 **範本作者**
   * 範本作者必須是 `template-authors` 群組。
* 頁面範本會保留與任何使用它們建立的頁面的動態連線。 這可確保對範本所做的任何變更都會反映在頁面本身中。
* 頁面範本讓頁面元件變得更通用，以便無需自訂即可使用核心頁面元件。

使用「頁面範本」，建立頁面的片段會隔離在元件中。 您可以在UI中設定必要的元件組合，因此不需要為每個頁面變數開發新的頁面元件。

本文档：

* 提供建立頁面範本的概觀
* 說明建立可編輯範本所需的管理員/開發人員工作
* 說明可編輯範本的技術基礎
* 說明AEM如何評估範本的可用性

>[!NOTE]
>
>本檔案假設您已熟悉範本的建立和編輯。 請參閱撰寫檔案 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md)，其中會詳細說明向範本作者公開的可編輯範本的功能。

>[!TIP]
>
>[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 透過實作範例，深入探討如何使用頁面範本，對於瞭解如何在新專案中設定範本非常有用

## 建立新範本 {#creating-a-new-template}

建立頁面範本主要是透過完成 [範本主控台和範本編輯器](/help/sites-cloud/authoring/features/templates.md) 由範本作者執行。 本節提供此程式的概述，並在後面說明在技術層面上發生的情況。

建立新的可編輯範本時，您可以：

1. 建立 [範本的資料夾](#template-folders). 這不是強制性的，但建議使用最佳實務。
1. 選取 [範本型別](#template-type). 系統會複製此專案，以建立 [範本定義](#template-definitions).

   >[!NOTE]
   >
   >現成提供一系列範本型別。 您也可以 [建立您自己的網站特定範本型別](#creating-template-types) 如有需要。

1. 設定新範本的結構、內容原則、初始內容和版面配置。

   **结构**

   * 結構可讓您定義範本的元件和內容。
   * 無法在產生的頁面上移動範本結構中所定義的元件，也無法將其從任何產生的頁面中刪除。
   * 如果您希望頁面作者能夠新增和移除元件，請將段落系統新增至範本。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   如需結構的技術詳細資訊，請參閱 [結構](#structure) 於本檔案中。

   **策略**

   * 內容原則會定義元件的設計屬性。

      * 例如，可用的元件或最小/最大尺寸。
   * 這些適用於範本（以及使用範本建立的頁面）。

   如需範本作者如何定義原則的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   如需原則的技術詳細資訊，請參閱 [內容原則](#content-policies) 於本檔案中。

   **初始内容**

   * 初始內容定義根據範本首次建立頁面時顯示的內容。
   * 然後，頁面作者可以編輯初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   如需初始內容的技術細節，請參閱 [初始內容](#initial-content) 於本檔案中。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   如需範本作者如何定義範本配置的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   如需範本配置的技術詳細資訊，請參閱 [版面](#layout) 於本檔案中。

1. 啟用範本，然後允許其用於特定內容樹狀結構。

   * 您可以啟用或停用範本，讓頁面作者可以使用或無法使用此範本。
   * 可以使模板可用于或不可用于某些页面分支。

   如需範本作者如何啟用範本的詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   如需啟用範本的技術詳細資訊，請參閱 [為我們啟用和允許範本](#enabling-and-allowing-a-template-for-use)e在此檔案中

1. 使用它來建立內容頁面。

   * 使用範本建立新頁面時，靜態範本與可編輯範本之間沒有可見的差異和指示。
   * 對於頁面作者，程式是透明的。

   如需頁面作者如何使用範本建立頁面的詳細資訊，請參閱 [建立及組織頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   如需使用可編輯的範本建立頁面的技術詳細資訊，請參閱 [結果內容頁面](#resultant-content-pages) 於本檔案中。

>[!TIP]
>
>切勿在模板中输入任何需要国际化的信息。基於內部化的目的， [核心元件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 建議使用。

>[!NOTE]
>
>模板是简化页面创建工作流的强大工具。不过，太多的模板会让作者不知所措，并使页面创建变得混乱。一个好的经验法则是将模板的数量保持在 100 个以内。
>
>由于潜在的性能影响，Adobe 建议不要使用超过 1000 个模板。

>[!NOTE]
>
>編輯器使用者端程式庫假設存在 `cq.shared` 名稱空間時，如果不存在，則會發生JavaScript錯誤 `Uncaught TypeError: Cannot read property 'shared' of undefined` 將產生。
>
>所有範例內容頁面都包含 `cq.shared`，因此任何以它們為基礎的內容都會自動包含 `cq.shared`. 但是，如果您決定從頭開始建立自己的內容頁面，而不是以範例內容為基礎，則必須確保包含 `cq.shared` 名稱空間。
>
>另請參閱 [使用使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md) 以取得進一步資訊。



## 範本資料夾 {#template-folders}

若要組織範本，您可以使用下列資料夾：

* `global`
* 特定網站

>[!NOTE]
>
>即使您可以巢狀內嵌資料夾，當使用者在 **範本** 主控台以平面結構呈現。

在標準AEM執行個體中 `global` 資料夾已存在於範本主控台中。 此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。您可以將預設範本新增至此資料夾或建立新資料夾（建議選項）。

>[!NOTE]
>
>最佳實務是建立新資料夾來存放自訂範本，而不是使用 `global` 資料夾。

>[!CAUTION]
>
>資料夾必須由使用者建立，具有 `admin` 權利。

範本型別和原則會根據下列優先順序繼承至所有資料夾：

1. 目前的資料夾
1. 目前資料夾的父系
1. `/conf/global`
1. `/apps`
1. `/libs`

將會建立所有允許專案的清單。 如果任何設定重疊( `path`/ `label`)，則只會向使用者顯示最接近目前資料夾的執行個體。

若要建立新資料夾，您可以執行下列任一項作業：

* 以程式設計方式或CRXDE Lite
* 使用 [設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以程式設計方式或CRXDE Lite方式為您的執行個體建立新資料夾（在/conf下）。

   必須使用下列結構：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然後，您可以在資料夾根節點上定義下列屬性：

   `<your-folder-name> [sling:Folder]`

   * 名称: `jcr:title`
   * 类型: `String`
   * 值：您要在「 」中顯示的「 」資料夾標題 **範本** 主控台。

1. 除了標準編寫許可權和許可權之外(例如， `content-authors`)您現在需要指派群組並定義作者所需的存取許可權(ACL)，才能在新資料夾中建立範本。

   此 `template-authors` group是需要指派的預設群組。 請參閱區段 [ACL和群組](#acls-and-groups) 以取得詳細資訊。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用設定瀏覽器 {#using-the-configuration-browser}

1. 前往 **全域導覽** -> **工具** > [**設定瀏覽器**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   現有資料夾會列在左側，包括 `global` 資料夾。

1. 单击&#x200B;**创建**。
1. 在 **建立設定** 對話方塊需要設定下列欄位：

   * **標題**：提供設定資料夾的標題
   * **可編輯的範本**：勾選以允許在此資料夾中使用可編輯的範本

1. 按一下 **建立**

>[!NOTE]
>
>在 [設定瀏覽器，](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 您可以編輯全域資料夾並啟動 **可編輯的範本** 選項來建立此資料夾中的範本，但這並非建議的最佳作法。

### ACL和群組 {#acls-and-groups}

建立範本資料夾後（透過CRXDE或使用設定瀏覽器），必須為範本資料夾的適當群組定義ACL，以確保適當的安全性。

的範本資料夾 [wknd教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 可作為範例。

#### 範本 — 作者群組 {#the-template-authors-group}

此 `template-authors` group是用來管理範本存取的群組，且隨附於AEM，但為空白。 必須將使用者新增至專案/網站的群組。

>[!CAUTION]
>
>此 `template-authors` 群組僅適用於必須能夠建立新範本的使用者。
>
>編輯範本的功能非常強大，如果不適當地完成，現有的範本可能會失效。 因此，此角色應著重於且僅包含合格使用者。

下表詳細說明範本編輯的必要許可權。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/群組</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>範本作者<br /> </td>
   <td>讀取、寫入、復寫</td>
   <td>在特定網站中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取範本</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>replicate內容作者在啟動頁面時需要啟動頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀取、寫入、復寫</td>
   <td>在特定網站中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取原則</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>啟用頁面時，內容作者需要啟用頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據預先定義的範本型別之一建立新範本。</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>无</td>
   <td>匿名Web使用者不得存取範本型別</td>
  </tr>
 </tbody>
</table>

此預設值 `template-authors` 群組僅涵蓋專案設定，其中所有 `template-authors` 允許成員存取及編寫所有範本。 對於更複雜的設定，需要多個範本作者群組來分隔範本的存取許可權，則必須建立更多自訂範本作者群組。 不過，範本作者群組的許可權仍會相同。

## 範本型別 {#template-type}

建立新範本時，您需要指定範本型別：

* 範本型別可有效提供範本的範本。 建立新範本時，會使用所選範本型別的結構和初始內容來建立新範本。

   * 範本型別會複製以建立範本。
   * 複製一旦發生，範本和範本型別之間的唯一連線是靜態參考，以供參考。

* 範本型別可讓您定義：

   * 頁面元件的資源型別。
   * 根節點的原則，定義範本編輯器中允許的元件。
   * 建議為回應式格線定義中斷點，並在範本型別上設定行動模擬器。

* AEM提供少量現成可用的範本型別，例如「HTML5頁面」和「最適化表單頁面」。

   * 提供其他範例作為的一部分 [wknd教學課程。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 範本型別通常由開發人員定義。

現成的範本型別儲存在下列位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得變更 `/libs` 路徑。 這是因為 `/libs` 可隨時透過AEM更新覆寫。

您的網站特定範本型別應儲存在類似位置：

* `/apps/settings/wcm/template-types`

自訂範本型別的定義應儲存在使用者定義的資料夾中（建議使用），或是儲存在 `global`. 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>範本型別必須遵循正確的資料夾結構(即 `/settings/wcm/...`)，否則將無法找到範本型別。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### 建立範本型別 {#creating-template-types}

如果您已建立可作為其他範本基礎的範本，則可以複製此範本作為範本型別。

1. 建立範本，就像建立任何頁面範本一樣 [如此處的紀錄](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)，這會作為範本型別的基礎。
1. 使用CRXDE Lite，複製新建立的範本 `templates` 節點至 `template-types` 下的節點 [範本資料夾](#template-folders).
1. 從刪除範本 `templates` 下的節點 [範本資料夾](#template-folders).
1. 在範本的副本中，位於 `template-types` 節點，全部刪除 `cq:template` 和 `cq:templateType` 全部屬性 `jcr:content` 節點。

您也可以使用GitHub提供的範例可編輯範本作為基礎，來開發自己的範本型別。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sites-example-custom-template-type專案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 範本定義 {#template-definitions}

可編輯範本的定義已儲存 [使用者定義的資料夾](#template-folders) （建議使用）或選擇使用 `global`. 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

範本的根節點為型別 `cq:Template` 骨架結構為：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素包括：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr：content {#jcr-content}

此節點保留範本的屬性：

* **名称**: `jcr:title`
* **名称**: `status`
   * ``**类型**: `String`
   * **值**： `draft`， `enabled` 或 `disabled`

### 结构 {#structure}

定義結果頁面的結構：

* 與初始內容合併( `/initial`)建立新頁面時。
* 對結構所做的變更將反映在使用範本建立的任何頁面中。
* 此 `root` ( `structure/jcr:content/root`)節點會定義產生頁面中可用的元件清單。
   * 範本結構中定義的元件無法在任何結果頁面上移動或刪除。
   * 解鎖元件後， `editable` 屬性已設定為 `true`.
   * 解鎖已包含內容的元件後，此內容將移至 `initial` 分支。

* 此 `cq:responsive` 節點保留回應式佈局的定義。

### 初始内容 {#initial-content}

定義建立新頁面時將具有的初始內容：

* 包含 `jcr:content` 複製到任何新頁面的節點。
* 與結構合併( `/structure`)建立新頁面時。
* 如果在建立後變更初始內容，則不會更新任何現有頁面。
* 此 `root` node會儲存元件清單，以定義結果頁面中可用的元件。
* 如果在結構模式下將內容新增到元件，且隨後解鎖該元件（反之亦然），則此內容會用作初始內容。

### 布局 {#layout}

時間 [編輯範本您可以定義版面](/help/sites-cloud/authoring/features/templates.md)，這會使用 [標準回應式佈局](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### 內容原則 {#content-policies}

內容原則會定義元件的設計屬性。 例如，可用的元件或最小/最大尺寸。 這些適用於範本（以及使用範本建立的頁面）。 可在範本編輯器中建立和選取內容原則。

* 屬性 `cq:policy`，位於 `root` 節點
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
提供頁面段落系統內容原則的相對參照。

* 屬性 `cq:policy`，於下的元件明確節點上 `root`，提供個別元件原則的連結。

* 實際原則定義儲存在下列位置：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>原則定義的路徑取決於元件的路徑。 `cq:policy` 保留組態本身的相對參照。

### 页面策略 {#page-policies}

頁面原則可讓您定義 [內容原則](#content-policies) 頁面（主要parsys）的範本或結果頁面中。

### 啟用和允許使用範本 {#enabling-and-allowing-a-template-for-use}

1. **啟用範本**

   使用範本之前，必須透過以下任一方式啟用它：

   * [啟用範本](/help/sites-cloud/authoring/features/templates.md) 從 **範本** 主控台。

   * 在上設定狀態屬性 `jcr:content` 節點。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 型別：字串
         * 价值: `enabled`

1. **允许的模板**

   * [在上定義允許的範本路徑 **頁面屬性**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) 子分支的適當頁面或根頁面的URL。
   * 設定屬性：
      `cq:allowedTemplates`
於 
`jcr:content` 必要分支的節點。
   例如，其值為：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 結果內容頁面 {#resultant-content-pages}

從可編輯範本建立的頁面：

* 使用合併的子樹狀結構建立 `structure` 和 `initial` 在範本中

* 具有範本和範本型別中所儲存資訊的參考。 這是透過以下專案達成： `jcr:content` 具有下列屬性的節點：

   * `cq:template`  — 提供實際範本的動態參考；讓範本的變更反映在實際頁面上。

   * `cq:templateType`  — 提供範本型別的參考。

![範本、內容和元件如何相互關聯](assets/templates-content-components.png)

上圖顯示範本、內容和元件如何相互關聯：

* 控制器 —  `/content/<my-site>/<my-page>`  — 參照範本的結果頁面。 內容會控制整個程式。 根據定義，它會存取適當的範本和元件。
* 設定 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [範本和相關內容原則](#template-definitions) 定義頁面設定。
* 模型 — OSGi套件組合 —  [OSGI套件組合](/help/implementing/deploying/configuring-osgi.md) 實作功能。
* 檢視 —  `/apps/<my-site>/components`  — 在製作和發佈環境中，內容會由元件轉譯。

轉譯頁面時：

* **模板**:

   * 此 `cq:template` 其屬性 `jcr:content` 節點將被引用，以存取與該頁面對應的範本。

* **组件**:

   * 頁面元件會合併 `structure/jcr:content` 範本的樹狀結構，具有 `jcr:content` 頁面的樹狀結構。
      * 頁面元件僅可讓作者編輯已標籤為可編輯的範本結構節點（以及任何子系）。
      * 在頁面上呈現元件時，該元件的相對路徑將取自 `jcr:content` 節點；下方的相同路徑 `policies/jcr:content` 接著會搜尋範本的節點。
         * 此 `cq:policy` 此節點的屬性指向實際內容原則（即它儲存該元件的設計設定）。
            * 這可讓您擁有重複使用相同內容原則設定的多個範本。

### 模板可用性 {#template-availability}

在網站管理介面中建立新頁面時，可用範本的清單取決於新頁面的位置以及每個範本中指定的版位限制。

下列屬性決定是否使用範本 `T` 允許用於要放置為頁面子項的新頁面 `P`. 以下每個屬性都是多值字串，其中包含零個或多個用來與路徑比對的規則運算式：

* 此 `cq:allowedTemplates` 的屬性 `jcr:content` 的子節點： `P` 或祖先 `P`.

* 此 `allowedPaths` 屬性 `T`.

* 此 `allowedParents` 屬性 `T`.

* 此 `allowedChildren` 的範本屬性 `P`.

評估的運作方式如下：

* 第一個非空白 `cq:allowedTemplates` 將頁面階層從開頭遞增時發現屬性 `P` 比對的路徑 `T`. 如果沒有任何相符的值， `T` 已拒絕。

* 若 `T` 具有非空白 `allowedPaths` 屬性，但沒有值符合的路徑 `P`， `T` 已拒絕。

* 如果上述兩個屬性都空白或不存在， `T` 除非屬於與相同的應用程式，否則會遭拒 `P`. `T` 屬於與相同的應用程式 `P` 若且唯若第二層路徑的名稱 `T` 與路徑的第二層級名稱相同 `P`. 例如，範本 `/apps/wknd/templates/foo` 屬於與頁面相同的應用程式 `/content/wknd`.

* 若 `T` 具有非空白 `allowedParents` 屬性，但沒有值符合的路徑 `P`， `T` 已拒絕。

* 如果範本屬於 `P` 具有非空白 `allowedChildren` 屬性，但沒有值符合的路徑 `T`， `T` 已拒絕。

* 在所有其他情況下， `T` 允許。

下圖說明範本評估程式：

![範本評估程式](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM提供多個屬性，可控制底下允許的範本 **網站**. 不過，將它們合併可能會導致非常複雜的規則，而且難以追蹤和管理。
>
>因此，Adobe建議您先定義：
>
>* 僅限 `cq:allowedTemplates` 屬性
>
>* 僅於網站根目錄上
>
>如需範例，請參閱 [wknd教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 內容： `/content/wknd/jcr:content`
>
>屬性 `allowedPaths`， `allowedParents`、和 `allowedChildren` 亦可放置在範本上，以定義更複雜的規則。 不過，如果可能的話，它會 *很多* 更簡單以進一步定義 `cq:allowedTemplates` 網站子區段上的屬性（如果需要進一步限制允許的範本）。
>
>另一個優點是 `cq:allowedTemplates` 作者可以在以下位置更新屬性： **進階** 的標籤 **頁面屬性**. 其他範本屬性無法使用（標準） UI更新，因此需要開發人員維護規則和每次變更的程式碼部署。

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用於在指定頁面下建立子頁面，請使用 `cq:allowedTemplates` 屬性 `jcr:content` 頁面節點，用來指定允許做為子頁面的範本清單。 例如，清單中的每個值都必須是允許的子頁面範本的絕對路徑 `/apps/wknd/templates/page-content`.

您可以使用 `cq:allowedTemplates` 範本的屬性  `jcr:content` 節點，將此設定套用至使用此範本的所有新建立頁面。

如果您想要新增更多限制，例如關於範本階層的限制，您可以使用 `allowedParents/allowedChildren` 範本的屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項/子項。
