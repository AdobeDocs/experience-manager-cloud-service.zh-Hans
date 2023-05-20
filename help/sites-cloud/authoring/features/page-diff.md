---
title: 页面差异
description: 頁面差異功能可方便並排比較兩個頁面，並反白顯示其差異。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 42%

---

# 页面差异 {#page-diff}

## 简介 {#introduction}

內容建立是一個反複的過程。 以效率撰寫需要能夠檢視反複專案之間有何變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易出錯。 作者希望能夠輕鬆地將目前頁面與另一個版本並排比較。

頁面差異功能可方便並排比較兩個頁面，並反白顯示其差異。

>[!NOTE]
>
>用户必须具有针对节点 `/content/versionhistory` 的&#x200B;**修改/创建/删除**&#x200B;权限，才能使用此功能。
>
>请参阅[开发和页面差异](/help/implementing/developing/introduction/page-diff.md#operation-details)，以了解有关此功能的更多技术详细信息。

## 使用 {#use}

可以并排比较以下内容：

* [版本](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - 将页面的以前版本与其当前状态进行比较
* [Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) – 将 Live Copy 与其 Blueprint 进行比较
* [启动项](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) – 将启动项与其源进行比较
* [语言副本](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) – 将翻译之前和翻译之后（重新翻译）的页面进行比较

請參閱相關主題，瞭解如何在這些內容中開始差異化。

### 差異的表示 {#presentation-of-differences}

無論比較的內容為何，差異的顯示方式會維持不變。

* 開始差異時選取的內容會顯示在左側（差異進入點）。
* 比較對象內容會顯示在右側（所選內容會與之比較）。

例如，如果比較版本，目前版本會顯示在左側，而先前版本會顯示在右側。

兩個頁面的來源會清楚顯示在瀏覽器視窗頂端的標頭列中。

![版本并排视图](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差異會偵測元件和HTML層級的變更。 已變更的專案會以不同的顏色反白。

**元件變更**

* 淡綠色 — 已新增元件
* 粉紅色 — 元件已移除

**HTML變更**

* 深綠色 — 新增HTML
* 红色 - 删除了 HTML

>[!NOTE]
>
>比較語言副本時，反白顯示會停用，因為在翻譯中，所有變更和反白顯示都沒有好處。

### 全熒幕和正在退出 {#fullscreen-and-exiting}

为了集中查看特定内容，您可以单击并排差异比较任何一侧的全屏图标，以将其放大到整个浏览器窗口。

![全屏按钮](/help/sites-cloud/authoring/assets/versions-full-screen.png)

选定的一侧将填满整个窗口，但标题栏仍将保留在顶部，允许您在两个页面之间切换。

![全屏模式](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>如果浏览器宽度不能同时容纳处于全屏视图中的两个页面名称，则只会显示所显示页面的名称，而其他名称将显示在省略号后面。

您也可以选择单击退出全屏图标来关闭全屏视图。

![退出全屏模式](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

您可以隨時按一下標頭中的「關閉」按鈕來結束並排比較。

## 限制 {#limitations}

在某些情況下，頁面差異可能不會如預期偵測到差異。

* 不同版本和啟動時，差異不會將階層連結、選單、產品清單或標誌（依賴網站結構來呈現其內容的元件）等動態元件列入考量。
* 对于版本，差异不会重新创建访问控制策略和 Live Copy 关系。
* 如果頁面已移動，您將無法再執行與移動前所做的任何版本之間的差異。
   * 如果您遇到差异问题，请检查页面的[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)以查看页面是否已被移动。

>[!NOTE]
>
>各版本之间不能相互进行比较。只能将页面的当前版本与其他版本进行比较。当前版本始终是突出显示更改的版本。

>[!NOTE]
>
>如需有關頁面差異機制的操作以及可能影響頁面差異的限制的詳細資訊，請參閱 [開發人員檔案](/help/implementing/developing/introduction/page-diff.md) 此功能的功能。
