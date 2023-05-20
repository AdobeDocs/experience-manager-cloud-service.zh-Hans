---
title: AEM UI 的结构
description: AEM UI具有數個基本原則，且由數個關鍵元素組成
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 4%

---

# AEM UI 的结构 {#structure-of-the-aem-ui}

AEM UI具有數個基本原則，並由數個關鍵元素組成：

## 控制台 {#consoles}

### 基本版面與調整大小 {#basic-layout-and-resizing}

UI同時適用於行動裝置和桌上型裝置，不過AEM並非建立兩種樣式，而是使用一種適用於所有熒幕和裝置的樣式。

所有模組都使用相同的基本版面，在AEM中這可以視為：

![AEM Sites主控台](assets/ui-sites-console.png)

版面配置會遵循回應式設計樣式，並配合您所使用的裝置/視窗大小。

例如，當解析度低於1024px （如同在行動裝置上）時，顯示器將會相應地調整：

![網站主控台行動裝置檢視](assets/ui-sites-mobile.png)

### 标题栏 {#header-bar}

![AEM標頭列](assets/ui-header-bar.png)

標題列會顯示全域元素，包括：

* 標誌和您目前使用的特定產品/解決方案；對於AEM，這也形成指向全域導覽的連結
* 搜索
* 用於存取說明資源的圖示
* 存取其他解決方案的圖示
* 任何等待您的警報或收件匣專案的指標（及存取權）
* 使用者圖示，以及設定檔管理的連結

### 工具栏 {#toolbar}

工具列與您的位置及表面工具相關，這些工具與控制以下頁面中的檢視或資產相關。 工具列是產品專屬的，但元素有一些共同之處。

工具列會在任何位置顯示目前可用的動作：

![AEM Sites工具列](assets/ui-sites-toolbar.png)

也取決於目前是否選取資源：

![已選取AEM Sites工具列](assets/ui-sites-toolbar-selected.png)

### 左边栏 {#left-rail}

您可以視需要開啟/隱藏左側邊欄，以顯示：

* **仅限内容**
* **内容树**
* **时间线**
* **引用**
* **过滤器**

預設值為 **僅內容** （欄隱藏）。

![左边栏](assets/ui-left-rail.png)

## 页面创作 {#page-authoring}

編寫頁面時，結構區域如下。

### 内容框架 {#content-frame}

頁面內容會在內容框架中呈現。 內容框架完全獨立於編輯器 — 以確保不會因CSS或JavaScript而發生衝突。

內容框架位於視窗的右側區段、工具列下方。

![內容框架](assets/ui-content-frame.png)

### 編輯器框架 {#editor-frame}

編輯器框架會啟用編輯功能。

編輯器框架是所有頁面製作元素的容器（抽象）。 它位在內容框架頂端，並包括：

* 顶部工具栏
* 側面板
* 所有覆蓋
* 任何其他頁面製作元素；例如，元件工具列

![編輯器框架](assets/ui-editor-frame.png)

### 側面板 {#side-panel}

這包含三個預設標籤。 此 **資產** 和 **元件** 定位點可讓您選取這類元素，並將它們從面板拖放至頁面上。 此 **內容樹狀結構** 索引標籤可讓您檢查頁面上內容的階層。

側面板預設為隱藏。 選取時，它將顯示在左側，或滑過以覆蓋整個視窗，當視窗大小低於1024px的寬度；例如，在行動裝置上。

![側面板](assets/ui-side-panel.png)

### 側面板 — 資產 {#side-panel-assets}

在「資產」標籤中，您可以從資產範圍中選取。 您也可以篩選特定字詞，或選取群組。

![資產標籤](assets/ui-side-panel-assets.png)

### 側面板 — 資產群組 {#side-panel-asset-groups}

「資產」標籤中有一個下拉式清單，可用來選取特定資產群組。

![資產群組](assets/ui-side-panel-asset-groups.png)

### 側面板 — 元件 {#side-panel-components}

在「元件」標籤中，您可以從元件範圍中選取。 您也可以篩選特定字詞，或選取群組。

![元件標籤](assets/ui-side-panel-components.png)

### 側面板 — 內容樹狀結構 {#side-panel-content-tree}

在「內容樹狀結構」標籤中，您可以檢視頁面上內容的階層。 按一下索引標籤中的專案會跳至，並在編輯器內選取頁面上的專案。

![内容树](assets/ui-side-panel-content-tree.png)

### 叠加 {#overlays}

這些會覆蓋內容框架，並由 [圖層](#layer) 瞭解如何與元件及其內容互動（完全透明）的機制。

這些覆蓋圖會在編輯器框架中顯示（包含所有其他頁面製作元素），但實際上會在內容框架中覆蓋適當的元件。

![叠加](assets/ui-overlays.png)

### 圖層 {#layer}

圖層是獨立的功能組合，可啟動至：

* 提供頁面的不同檢視
* 允許您操控和/或與頁面互動

這些圖層為整個頁面提供了複雜的功能，而不是為個別元件執行特定動作。

AEM隨附數個已實作用於頁面編寫的圖層；例如，包括編輯、預覽和註釋圖層。

>[!NOTE]
>
>圖層是一個強大的概念，可影響使用者對頁面內容的檢視以及與頁面內容的互動。 開發自己的圖層時，您需要確保圖層在退出時進行清除。

### 圖層切換器 {#layer-switcher}

圖層切換器可讓您選擇要使用的圖層。 當關閉時，它會指出目前使用的圖層。

圖層切換器可從工具列（位於視窗頂端、編輯器框架內）以下拉式清單的形式提供。

![圖層切換器](assets/ui-layer-switcher.png)

### 组件工具栏 {#component-toolbar}

每個元件例項在按一下後都會顯示其工具列（按一下或緩慢按兩下）。 工具列包含頁面上元件執行個體可用的特定動作（例如，複製、貼上、開啟編輯器）。

根據可用的空間，元件工具列會放置在適當元件的右上角或右下角。

![组件工具栏](assets/ui-component-toolbar.png)

## 更多信息 {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

如需進一步的技術資訊，請參閱 [JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) 用於頁面編輯器。
