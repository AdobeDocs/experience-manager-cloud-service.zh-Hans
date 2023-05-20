---
title: 创作环境和工具
description: AEM 的创作环境提供了各种可用于组织和编辑内容的机制
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 57%

---

# 创作环境和工具 {#authoring-the-environment-and-tools}

AEM 的创作环境提供了各种可用于组织和编辑内容的机制。可以从各种控制台和页面编辑器访问提供的工具。

## 管理您的站点 {#managing-your-site}

**站点**&#x200B;控制台允许您使用标题栏、工具栏、操作图标（适用于所选资源）和痕迹导航来导航和管理您的网站，选择后还可使用辅助边栏（例如时间线和引用）。

例如，列视图：

![列视图](/help/sites-cloud/authoring/assets/column-view.png)

## 编辑页面内容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![页面编辑器](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>第一次開啟頁面進行編輯時，系統會提供一系列投影片來導覽功能。
>
>您可以視需要略過導覽，並隨時透過選擇 **頁面資訊** 功能表。

## 访问帮助 {#accessing-help}

在编辑页面时，**帮助**&#x200B;可从以下位置访问：

* [**页面信息**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties)&#x200B;选择器，这将显示幻灯片介绍（在您第一次访问编辑器时显示）
* 适用于特定组件的[配置](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)对话框（使用对话工具栏中的 ? 图标），其中将显示上下文相关帮助

進一步的 [說明相關資源可從主控台取得](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## 元件瀏覽器 {#components-browser}

组件是 AEM 内容的构建基块。您可以将多个组件放在一个页面上并配置其选项，以便使用 AEM 构建内容页面。

元件瀏覽器會顯示可在目前頁面上使用的所有元件。 這些檔案可以拖曳至適當位置，然後編輯以新增您的內容。

组件浏览器是侧面板中的一个选项卡（侧面板中还有[资产浏览器](#assets-browser)和[内容树](#content-tree)）。要打开（或关闭）侧面板，请使用工具栏左上方的图标：

![侧面板切换](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它將從左側滑開(選取 **元件** 索引標籤（如有需要）。 開啟時，您可以瀏覽頁面可用的所有元件。

实际外观和操作取决于您所使用的设备类型：

* **移动设备（例如 iPad）**

   元件瀏覽器會完整涵蓋正在編輯的頁面。

   若要新增元件至頁面，請按住所需元件並向右移動，元件瀏覽器將關閉並重新顯示頁面 — 您可以在此處放置元件。

   ![移动设备上的组件浏览器](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **案頭裝置**

   元件瀏覽器會在視窗左側開啟。

   若要新增元件至頁面，請按一下所需元件，然後將其拖曳至所需位置。

   ![桌面设备上的组件浏览器](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   元件表示方式：

   * 元件名稱
   * 组件组（灰色）
   * 圖示或縮寫
      * 標準元件的圖示為單色。
      * 缩写始终由组件名称的前两个字符组成。

   从&#x200B;**组件**&#x200B;浏览器顶部的工具栏可以：

   * 按名称筛选组件。
   * 使用下拉选择框将显示内容限定为特定组。

   有关组件的更多详细说明，您可以单击或点按&#x200B;**组件**&#x200B;浏览器（如果可用）中组件旁边的信息图标。例如，对于&#x200B;**内容片段**：

   ![组件浏览器信息](/help/sites-cloud/authoring/assets/component-browser-information.png)

   有关可供您使用的组件的更多信息，请参阅[组件控制台](/help/sites-cloud/authoring/features/components-console.md)。

>[!NOTE]
>
>當寬度小於1024畫素時會偵測到行動裝置。 小型案頭視窗亦可如此。

## 资产浏览器 {#assets-browser}

資產瀏覽器會顯示全部 [資產](/help/assets/home.md) 直接在您目前頁面上使用。

资产浏览器是侧面板中的一个选项卡，侧面板中还有[组件浏览器](#components-browser)和[内容树](#content-tree)。要打开或关闭侧面板，请使用工具栏左上角的图标：

![侧面板切换](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

打开侧面板时，它将从左侧滑开。根据需要选择&#x200B;**资产**&#x200B;选项卡。

![“资产浏览器”按钮](/help/sites-cloud/authoring/assets/assets-browser-button.png)

當資產瀏覽器開啟時，您可以瀏覽頁面可用的所有資產。 如有需要，可使用無限捲動來展開清單。

![资产浏览器](/help/sites-cloud/authoring/assets/assets-browser.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當型別的現有元件。
   * 例如，可以将图像类型的资产拖动到图像组件上。
* 段落系统中用于创建相应类型新组件的[占位符](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder)。
   * 例如，可以将图像类型的资产拖动到段落系统中，以创建图像组件。

>[!NOTE]
>
>這適用於特定資產和元件型別。 另請參閱 [使用「資產瀏覽器」插入元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) 以取得更多詳細資料。

從資產瀏覽器的頂端工具列，您可以依下列方式篩選資產：

* 名称
* 路径
* 资产类型，如图像、视频、文档、段落、内容片段和体验片段
* 资源特性，如方向和样式
   * 僅適用於特定資產型別

实际外观和操作取决于您所使用的设备类型：

* **移动设备**

   資產瀏覽器會完整涵蓋正在編輯的頁面。

   若要將資產新增至頁面，請觸控並按住所需資產，然後將其向右移動 — 資產瀏覽器將關閉並重新顯示頁面，您可以在其中將資產新增至所需元件。

   ![移动设备上的资产浏览器](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **桌面设备**

   資產瀏覽器會在視窗左側開啟。

   若要將資產新增至頁面，請按一下所需的資產，並將其拖曳至所需的元件或位置。

   ![桌面设备上的资产浏览器](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>在宽度小于 1024 像素时将视为检测到移动设备，这种情况也可能出现在较小的桌面窗口中。

如果您需要快速更改资产，可以直接从资产浏览器启动[资产编辑器](/help/assets/manage-digital-assets.md)，方法是单击资产名称旁边显示的编辑图标。

![资产编辑按钮](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 内容树 {#content-tree}

此 **內容樹狀結構** 提供階層中頁面所有元件的概觀，讓您一眼就能看到頁面的構成方式。

內容樹狀結構是側面板中的標籤（連同元件和資產瀏覽器）。 要打开（或关闭）侧面板，请使用工具栏左上方的图标：

![“内容树”按钮](/help/sites-cloud/authoring/assets/content-tree-button.png)

打开侧面板时，它将（从左侧）滑开。根据需要选择&#x200B;**内容树**&#x200B;选项卡。開啟時，您可以看到頁面或範本的樹狀檢視表示法，因此更容易瞭解其內容如何以階層方式建構。 此外，在複雜頁面上，它可讓您更輕鬆地在頁面的元件之間跳轉。

![内容树](/help/sites-cloud/authoring/assets/content-tree-editor.png)

页面可以由许多相同类型的组件轻松组成，因此内容（组件）树会在组件类型名称（黑色）之后显示描述性文本（灰色）。描述性文字來自元件的常見屬性，例如標題或文字。

元件型別將以使用者語言顯示，而元件說明文字則來自頁面語言。

按一下元件旁的>形箭號將會收合或展開該層級。

![内容树 V 形扩展](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

按一下元件即可在頁面編輯器中反白顯示該元件。 可用的動作取決於頁面狀態：

* 例如，基本頁面：

   ![突出显示的内容树](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   基本页面的组件将具有常用选项。

   如果您在樹狀結構中點選的元件可編輯，則名稱右側會出現扳手圖示。 按一下此圖示將直接啟動元件的編輯對話方塊。

   ![“内容树”编辑按钮](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* 属于 [livecopy](/help/sites-cloud/administering/msm/overview.md) 一部分且其中组件继承自其他页面的页面。

>[!NOTE]
>
>如果您正在浏览器宽度小于 1024 像素的移动设备上编辑页面，则内容树将不可用。

## 片段 – 关联的内容浏览器 {#fragments-associated-content-browser}

如果您的页面包含内容片段，那么您还可以访问[适用于关联内容的浏览器](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)。

## 引用 {#references}

**引用** 顯示所選頁面的連線：

* Blueprint
* 启动项
* Live Copy
* 语言副本
* 传入链接
* 对引用组件的使用：借入和借出的内容

打开所需的控制台，然后导航到所需资源并使用以下方法打开&#x200B;**引用**：

![引用选项](/help/sites-cloud/authoring/assets/references.png)

[选择您需要的资源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)以显示与该资源相关的引用类型列表：

![引用详细信息](/help/sites-cloud/authoring/assets/references-detail.png)

選取適當的參照型別以取得詳細資訊。 在某些情況下，當您選取特定參照時，可以使用進一步的動作，包括：

* **传入链接**，在选择特定链接后提供引用页面的页面列表，并可直接访问以&#x200B;**编辑**&#x200B;这些页面之一
* 使用&#x200B;**引用**&#x200B;组件的借入和借出内容的实例，您可以从此处导航至正在引用/引用的页面
* [启动项](/help/sites-cloud/authoring/launches/overview.md)，提供对相关启动项的访问权
* [Live Copy](/help/sites-cloud/administering/msm/overview.md) 显示基于选定资源的所有 Live Copy 的路径。
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md)，提供详细信息和各种操作
* [语言副本](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)，提供详细信息和各种操作

## 事件 – 时间线 {#events-timeline}

对于相应的资源（例如，**站点**&#x200B;控制台中的页面或&#x200B;**资产**&#x200B;控制台中的资产），[可使用时间轴显示任何选定项目上的近期活动](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)。

打开所需的控制台，然后导航到需要的资源并使用以下方法打开&#x200B;**时间线**：

![时间线选项](/help/sites-cloud/authoring/assets/timeline.png)

[选择您需要的资源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**活动**，可列出对所选资源的所有近期操作：

![时间线详细信息](/help/sites-cloud/authoring/assets/timeline-detail.png)

## 页面信息 {#page-information}

“页面信息”（均衡器图标）会打开一个菜单，其中也会提供有关上次编辑和上次发布的详细信息。根据页面、其站点和您的实例的特性，可用的选项可能会更多，也可能会更少：

![页面信息选项](/help/sites-cloud/authoring/assets/page-information.png)

* [打开属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [转出页](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [启动工作流](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [锁定页面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [取消发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [编辑模板](/help/sites-cloud/authoring/features/templates.md)
* [以发布的形式查看](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [以管理员身份查看](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [帮助](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [提升启动项](/help/sites-cloud/authoring/launches/promoting.md)（如果该页面是启动项）

此外， **頁面資訊** 可讓您在適當時存取analytics和建議。

## 頁面模式 {#page-modes}

編輯頁面時，有多種模式可允許不同的動作：

* [編輯](/help/sites-cloud/authoring/fundamentals/editing-content.md)  — 編輯頁面內容時使用的模式。
* [布局](/help/sites-cloud/authoring/features/responsive-layout.md) - 允许您创建和编辑依赖于设备的响应式布局（如果页面基于布局容器）
* [目標定位](/help/sites-cloud/authoring/personalization/targeted-content.md)  — 透過所有管道的目標定位和測量，提高內容關聯性。
* [時間扭曲](/help/sites-cloud/authoring/features/page-versions.md#timewarp)  — 可讓您檢視特定時間點的頁面狀態。
* [即時副本狀態](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status)  — 可讓您快速概覽即時副本狀態以及不會繼承哪些元件。
* [开发人员模式](/help/implementing/developing/tools/developer-mode.md)
* [预览](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) - 用于查看将在发布环境中显示的页面；或使用内容中的链接进行导航。
* [注释](/help/sites-cloud/authoring/fundamentals/annotations.md) - 用于在页面上添加或查看注释。

您可以使用右上角的图标访问这些模式。实际图标会因您当前所使用的模式而有所不同：

![页面模式](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* 視頁面特性而定，某些模式可能無法使用。
>* 存取某些模式需要適當的許可權。
>* 由於空間限制，開發人員模式不適用於行動裝置。
>* 使用[键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) (`Ctrl-Shift-M`) 可以在&#x200B;**预览**&#x200B;模式和当前选定的模式（例如，**编辑**、**布局**&#x200B;等）之间切换。
>


## 路径选择 {#path-selection}

通常在製作時，需要選取其他資源，例如定義指向其他頁面或資源的連結，或選取影像時。 若要輕鬆選取路徑， [路徑欄位](#path-fields) 優惠自動完成和 [路徑瀏覽器](#path-browser) 允許更強大的選擇。

### 路徑欄位 {#path-fields}

此處用來說明的範例是影像元件。 如需使用和編輯元件的詳細資訊，請參閱 [用於頁面編寫的元件](/help/sites-cloud/authoring/fundamentals/components.md).

路径字段现在具有自动完成和先行智能功能，可更方便地查找资源。

单击路径字段中的&#x200B;**打开选择对话框**&#x200B;按钮可打开[路径浏览器](#path-browser)对话框，以查看更多详细选择选项。

![“打开选择对话框”按钮](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

或者您可以在路径字段中开始输入，AEM 将会在您输入的同时提供匹配的路径。

![“打开选择对话框”按钮](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### 路径浏览器 {#path-browser}

路径浏览器的组织方式与站点控制台的[列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)相似，允许查看更多详细资源选择选项。

![路径浏览器](/help/sites-cloud/authoring/assets/path-browser.png)

* 選取資源後， **選取** 對話方塊右上角的按鈕會變成使用中。 按一下或點選以確認選取範圍或 **取消** 以中止。
* 如果上下文允许选择多个资源，则选择某个资源也会激活“选择 **** ”按钮，但也会将选定资源的计数添加到窗口的右上角。 单击该 **数字旁边的** X可取消选择全部。
* 當您瀏覽樹狀結構時，您的位置會反映在對話方塊頂端的階層連結中。 這些階層連結也可用來在資源階層內快速跳轉。
* 您可以隨時使用對話方塊頂端的搜尋欄位。 按一下 **X** 以清除搜尋。
* 要缩小搜索范围，您可以显示过滤器选项并按特定路径筛选结果。

   ![过滤器选项](/help/sites-cloud/authoring/assets/filters-option.png)

## 键盘快捷键 {#keyboard-shortcuts}

可以使用各种[键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)。
