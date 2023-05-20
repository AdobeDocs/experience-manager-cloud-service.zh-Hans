---
title: 在AEMas a Cloud Service上使用使用者端資料庫
description: AEM提供使用者端程式庫資料夾，可讓您將使用者端程式碼(clientlibs)儲存在存放庫中、將其組織成類別，以及定義每個類別程式碼何時及如何提供給使用者端
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 906fbefdbd100a7874b6f58ef23b7aaa46ac4ba3
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 1%

---


# 在AEMas a Cloud Service上使用使用者端資料庫 {#using-client-side-libraries}

數位體驗重度依賴由複雜JavaScript和CSS程式碼驅動的使用者端處理。 AEM使用者端程式庫(clientlibs)可讓您整理這些使用者端程式庫並將其集中儲存在存放庫中。 搭配 [AEM專案原型中的前端建置流程，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) AEM專案的前端程式碼管理變得簡單。

在AEM中使用clientlibs的優點包括：

* 使用者端程式碼會像其他所有應用程式程式碼和內容一樣儲存在存放庫中
* AEM中的Clientlibs可將所有CSS和JS彙總到一個檔案中
* 透過可存取的路徑公開clientlibs [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* 允許重寫參照檔案或影像的路徑

Clientlibs是內建的解決方案，可從AEM傳遞CSS和Javascript。

>[!TIP]
>
>為AEM專案建立CSS和Javascript的前端開發人員也應熟悉 [AEM專案原型及其自動化前端建置流程。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什麼是使用者端資料庫 {#what-are-clientlibs}

網站需要在使用者端處理JavaScript和CSS以及靜態資源（例如圖示和網頁字型）。 clientlib是用來參照（視需要依類別）及提供這類資源的AEM機制。

AEM會將網站的CSS和Javascript收集到一個位於中央位置的檔案中，以確保在HTML輸出中只會包含任何資源的一個副本。 這樣可最大化傳送效率，並透過Proxy將這類資源集中維護在存放庫中，確儲存取安全。

## AEMas a Cloud Service的前端開發 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端資產都應在 [AEM專案原型的ui.frontend模組。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的靈活性可讓您使用所選擇的現代化網頁工具來建立和管理這些資源。

然後，原型可以將資源編譯為單一CSS和JS檔案，並自動將其嵌入到 `cq:clientLibraryFolder` 存放庫中。

## 使用者端程式庫資料夾結構 {#clientlib-folders}

使用者端程式庫資料夾是型別的存放庫節點 `cq:ClientLibraryFolder`. 其定義於 [CND標籤法](https://jackrabbit.apache.org/node-type-notation.html) 是

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 節點可放置於 `/apps` 存放庫的子樹狀結構。
* 使用 `categories` 節點的屬性，用來識別其所屬的程式庫類別。

每個 `cq:ClientLibraryFolder` 會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下文）。 的重要屬性 `cq:ClientLibraryFolder` 的設定如下：

* `allowProxy`：由於所有clientlibs都必須儲存在 `apps`，此屬性可讓您透過Proxy servlet存取使用者端程式庫。 請參閱區段 [找到使用者端程式庫資料夾並使用Proxy使用者端程式庫Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下方的。
* `categories`：識別這個JS和/或CSS檔案集所屬的類別 `cq:ClientLibraryFolder` 秋天。 此 `categories` 屬性是多值屬性，可讓程式庫資料夾屬於多個類別（請參閱下方以瞭解其用處）。

如果使用者端程式庫資料夾包含一或多個來源檔案，在執行階段會將它們合併至單一JS和/或CSS檔案中。 產生檔案的名稱是節點名稱，帶有 `.js` 或 `.css` 副檔名。 例如，程式庫節點命名為 `cq.jquery` 產生的檔案中的結果命名為 `cq.jquery.js` 或 `cq.jquery.css`.

使用者端程式庫資料夾包含下列專案：

* JS和/或CSS來源檔案
* 支援CSS樣式的靜態資源，例如圖示、網頁字型等。
* 一 `js.txt` 檔案和/或一個 `css.txt` 可識別在產生的JS和/或CSS檔案中要合併之來源檔案的檔案

![Clientlib架構](assets/clientlib-architecture.drawio.png)

## 建立使用者端資料庫資料夾 {#creating-clientlib-folders}

使用者端程式庫必須位於 `/apps`. 這是為了將程式碼與內容和設定更好地隔離。

用於下的使用者端程式庫的順序 `/apps` 為了可存取，會使用proxy servelt。 ACL仍會在使用者端程式庫資料夾上強制執行，但servlet允許透過讀取內容 `/etc.clientlibs/` 如果 `allowProxy` 屬性已設定為 `true`.

1. 在網頁瀏覽器中開啟CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 選取 `/apps` 資料夾並按一下 **建立>建立節點**.
1. 輸入程式庫資料夾的名稱，然後在 **型別** 清單選取 `cq:ClientLibraryFolder`. 按一下 **確定** 然後按一下 **全部儲存**.
1. 若要指定程式庫所屬的類別，請選取 `cq:ClientLibraryFolder` 節點，新增以下屬性，然後按一下 **全部儲存**：
   * 名称: `categories`
   * 型別：字串
   * 值：類別名稱
   * 多個：已選取
1. 若要透過下方的Proxy存取使用者端程式庫 `/etc.clientlibs`，選取 `cq:ClientLibraryFolder` 節點，新增以下屬性，然後按一下 **全部儲存**：
   * 名称: `allowProxy`
   * 型別：布林值
   * 价值: `true`
1. 如果您需要管理靜態資源，請建立名為的子資料夾 `resources` 位於使用者端資料庫資料夾下方。
   * 如果您將靜態資源儲存在資料夾下以外的任何位置 `resources`，無法在發佈執行個體上參考這些變數。
1. 將來源檔案新增至程式庫資料夾。
   * 這通常是由以下專案的前端建置流程完成： [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 您可以視需要在子資料夾中組織來源檔案。
1. 選取使用者端程式庫資料夾，然後按一下 **「建立」>「建立檔案」**.
1. 在「檔案名稱」方塊中，鍵入下列其中一個檔案名稱，然後按一下「確定」：
   * **`js.txt`：** 使用此檔案名稱來產生JavaScript檔案。
   * **`css.txt`：** 使用此檔案名稱來產生階層式樣式表。
1. 開啟檔案並輸入下列文字，以識別來源檔案的根路徑：
   * `#base=*[root]*`
   * Replace `[root]` 相對於TXT檔案，包含來源檔案的資料夾路徑。 例如，當來源檔案與TXT檔案位於相同的資料夾時，請使用以下文字：
      * `#base=.`
   * 下列程式碼會將根設定為名為mobile的資料夾，位於 `cq:ClientLibraryFolder` 節點：
      * `#base=mobile`
1. 在以下行上 `#base=[root]`，鍵入相對於根的來源檔案路徑。 將每個檔案名稱放在單獨的一行上。
1. 按一下 **全部儲存**.

## 服務使用者端程式庫 {#serving-clientlibs}

一旦您的使用者端程式庫資料夾 [視需要設定，](#creating-clientlib-folders) 您可以透過proxy請求您的clientlibs。 例如：

* 您在中有clientlib `/apps/myproject/clientlibs/foo`
* 您有一個靜態影像，位於 `/apps/myprojects/clientlibs/foo/resources/icon.png`

此 `allowProxy` 屬性可讓您要求：

* clientlib透過 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 靜態影像透過 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 透過HTL載入使用者端資料庫 {#loading-via-htl}

一旦您的clientlibs成功儲存和管理在其使用者端資料庫資料夾中，即可透過HTL存取。

使用者端程式庫會透過AEM提供的helper範本載入，該範本可透過以下方式存取： `data-sly-use`. 此檔案中提供Helper範本，您可以透過來呼叫此範本 `data-sly-call`.

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

[請參閱HTL檔案](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 以取得透過HTL載入clientlibs的詳細資訊。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 作者與發佈的使用者端資料庫 {#clientlibs-author-publish}

AEM發佈執行個體上需要大部分的clientlibs。 也就是說，大部分clientlibs的目的是產生內容的一般使用者體驗。 對於發佈執行個體上的clientlibs， [前端建置工具](#fed-for-aemaacs) 可透過以下方式使用和部署： [如上所述的client library資料夾。](#creating-clientlib-folders)

不過，有時可能需要使用者端程式庫來自訂編寫體驗。 例如，自訂對話方塊可能需要將少量CSS或JS部署至AEM編寫執行個體。

### 管理作者上的使用者端程式庫 {#clientlibs-on-author}

如果您需要在作者上使用使用者端資料庫，可以在下方建立使用者端資料庫 `/apps` 使用與publish相同的方法，但直接寫在 `/apps/.../clientlibs/foo` ，而不需建立整個專案來管理。

然後，您可以將使用者端程式庫新增至現成可用的使用者端程式庫類別，以「連結」至編寫JS中。

## 偵錯工具 {#debugging-tools}

AEM提供數種用於偵錯和測試使用者端程式庫資料夾的工具。

### 探索使用者端資料庫 {#discover-client-libraries}

此 `/libs/cq/granite/components/dumplibs/dumplibs` 元件會產生系統上所有使用者端程式庫資料夾的資訊頁。 此 `/libs/granite/ui/content/dumplibs` 節點將元件作為資源型別。 若要開啟頁面，請使用下列URL （視需要變更主機和連線埠）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

資訊包括程式庫路徑和型別（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和管道中的程式庫。

### 檢視產生的輸出 {#see-generated-output}

此 `dumplibs` 元件包含測試選擇器，顯示產生的原始程式碼 `ui:includeClientLib` 標籤之間。 此頁面包含js、css和主題屬性之不同組合的程式碼。

1. 使用下列其中一種方法開啟「測試輸出」頁面：
   * 從 `dumplibs.html` 頁面上，按一下 **按一下這裡進行輸出測試** 文字。
   * 在網頁瀏覽器中開啟下列URL （視需要使用不同的主機和連線埠）：
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 預設頁面顯示沒有categories屬性值的標籤的輸出。
1. 若要檢視類別的輸出，請輸入使用者端程式庫的 `categories` 屬性並按一下 **提交查詢**.

## 其他使用者端資料庫資料夾功能 {#additional-features}

AEM中的使用者端程式庫資料夾支援許多其他功能。 不過，在AEMas a Cloud Service上不需要這些字元，因此不建議使用。 為了完整起見，此處列出它們。

>[!WARNING]
>
>AEMas a Cloud Service上並不需要這些使用者端資料庫資料夾的其他功能，因此不建議使用。 為了完整起見，此處列出它們。

### AdobeGraniteHTMLLibrary Manager {#html-library-manager}

其他使用者端程式庫設定可透過 **AdobeGraniteHTML程式庫管理員** 位於的系統主控台面板 `https://<host>:<port>/system/console/configMgr`)。

### 其他資料夾屬性 {#additional-folder-properties}

其他資料夾屬性包括允許控制相依性和內嵌，但通常不再需要它們，不建議使用：

* `dependencies`：這是此程式庫資料夾所相依的其他使用者端程式庫類別清單。 例如，假設有兩個 `cq:ClientLibraryFolder` 節點 `F` 和 `G`，如果檔案位於 `F` 需要在下列位置有另一個檔案： `G` 為了正常運作，至少一個 `categories` 之 `G` 應該屬於 `dependencies` 之 `F`.
* `embed`：用來內嵌其他程式庫中的程式碼。 If節點 `F` 嵌入節點 `G` 和 `H`，產生的HTML會是來自節點的內容串連 `G` 和 `H`.

### 連結至相依性 {#linking-to-dependencies}

當使用者端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 此 `ui:includeClientLib` 參照使用者端程式庫資料夾的標籤會讓HTML程式碼包含所產生程式庫檔案的連結以及相依性。

相依性必須是另一個 `cq:ClientLibraryFolder`. 若要識別相依性，請將屬性新增至 `cq:ClientLibraryFolder` 具有下列屬性的節點：

* **名稱：** 相依性
* **型別：** 字串[]
* **值：** 目前程式庫資料夾所依賴之cq：ClientLibraryFolder節點的categories屬性值。

例如， `/etc/clientlibs/myclientlibs/publicmain` 有相依於 `cq.jquery` 資料庫。 參考主要使用者端程式庫的頁面會產生HTML，其中包含下列程式碼：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫內嵌程式碼 {#embedding-code-from-other-libraries}

您可以將使用者端程式庫的程式碼內嵌到另一個使用者端程式庫中。 在執行階段中，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

內嵌程式碼對於存取儲存在存放庫的安全區域中的資料庫很有用。

#### 應用程式專屬的使用者端程式庫資料夾 {#app-specific-client-library-folders}

最佳實務是將所有應用程式相關檔案保留在以下應用程式資料夾中 `/apps`. 拒絕網站訪客存取 `/apps` 資料夾。 若要同時滿足這兩個最佳實務，請在下方建立使用者端程式庫資料夾 `/etc` 嵌入以下使用者端資料庫的資料夾 `/apps`.

使用categories屬性來識別要內嵌的使用者端程式庫資料夾。 若要內嵌程式庫，請在內嵌中新增屬性 `cq:ClientLibraryFolder` 節點，使用下列屬性屬性：

* **名稱：** 內嵌
* **型別：** 字串[]
* **值：** 的categories屬性的值 `cq:ClientLibraryFolder` 要內嵌的節點。

#### 使用內嵌將請求最小化 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現發佈執行個體針對典型頁面產生的最終HTML包含相對大量的 `<script>` 元素。

在這種情況下，將所有必要的使用者端程式庫程式碼合併為單一檔案會很有用，這樣就能減少頁面載入時的來回請求數量。 若要這麼做，您可以 `embed` 必要的程式庫會使用「 」的內嵌屬性，將您的應用程式專屬的使用者端程式庫中 `cq:ClientLibraryFolder` 節點。

#### CSS檔案中的路徑 {#paths-in-css-files}

內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫 `/etc/client/libraries/myclientlibs/publicmain` 內嵌 `/apps/myapp/clientlib` 使用者端資源庫：

此 `main.css` 檔案包含下列樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS檔案會 `publicmain` 節點會使用原始影像的URL產生包含以下樣式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 請參閱HTML輸出中的內嵌檔案 {#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌使用者端程式庫產生預期的結果，您可以檢視執行階段內嵌的檔案名稱。 若要檢視檔案名稱，請附加 `debugClientLibs=true` 網頁URL的引數。 產生的程式庫包含 `@import` 陳述式，而非內嵌程式碼。

在上一個範例中 [從其他程式庫內嵌程式碼](#embedding-code-from-other-libraries) 區段， `/etc/client/libraries/myclientlibs/publicmain` client library資料夾內嵌 `/apps/myapp/clientlib` 使用者端資料庫資料夾。 將引數附加至網頁會在網頁的原始程式碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟 `publicmain.css` file會顯示下列程式碼：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL：
   * `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下提供為連結元素href的連結，開啟檔案並檢視原始程式碼。

### 使用前置處理器 {#using-preprocessors}

AEM支援可插拔的前處理器，並隨附以下支援 [YUI壓縮程式](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 適用於CSS和JavaScript及 [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) YUI設為AEM預設前置處理器的JavaScript。

可插拔的前處理器可彈性使用，包括：

* 定義可以處理指令碼來源的ScriptProcessors
* 處理器可設定選項
* 處理器可用於縮制，也可用於非縮制的情況
* clientlib可以定義要使用的處理器

>[!NOTE]
>
>依預設，AEM會使用YUI壓縮程式。 請參閱 [YUI Compressor GitHub檔案](https://github.com/yui/yuicompressor/issues) 以取得已知問題的清單。 切換至特定clientlibs的GCC壓縮程式可以解決使用YUI時觀察到的一些問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入使用者端程式庫中。 改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

#### 用途 {#usage}

您可以選擇針對每個clientlibrary或系統範圍設定前置處理器組態。

* 新增多值屬性 `cssProcessor` 和 `jsProcessor` 在clientlibrary節點上
* 或透過以下方式定義系統預設設定： **HTML程式庫管理員** OSGi設定

clientlib節點上的前置處理器設定優先於OSGI設定。

#### 格式與範例 {#format-and-examples}

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### CSS縮制的YUI壓縮程式和JS的GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 輸入指令碼以預先處理，然後使用GCC以縮小和模糊化 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### 其他GCC選項 {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

如需GCC選項的詳細資訊，請參閱 [GCC檔案](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### 設定系統預設縮制器 {#set-system-default-minifier}

YUI已設定為AEM中的預設縮制器。 若要將此變更為GCC，請按照以下步驟操作。

1. 前往Apache Felix設定管理員，網址為(`http://<host>:<portY/system/console/configMgr`)
1. 尋找並編輯 **AdobeGraniteHTML程式庫管理員**.
1. 啟用 **最小化** 選項（如果尚未啟用）。
1. 設定值 **JS處理器預設設定** 至 `min:gcc`.
   * 例如，如果以分號分隔，則可以傳遞選項， `min:gcc;obfuscate=true`.
1. 按一下 **儲存** 以儲存變更。
