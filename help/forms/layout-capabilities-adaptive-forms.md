---
title: Adaptive Forms的版面配置功能
seo-title: Layout capabilities of Adaptive Forms
description: Adaptive Forms在各種裝置上的版面配置與外觀是由版面配置設定所控管。 瞭解各種版面以及如何套用它們。
exl-id: e30c6ff9-692b-4415-8f14-b4ef616b2d12
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Adaptive Forms的版面配置功能 {#layout-capabilities-of-adaptive-forms}

[!DNL Adobe Experience Manager] 可讓您建立簡單易用的最適化Forms，為使用者提供動態體驗。 表單版面配置會控制專案或元件在最適化表單中的顯示方式。

<!-- ## Prerequisite knowledge {#prerequisite-knowledge}

Before learning about the different layout capabilities of Adaptive Forms, read [Introduction to authoring forms](introduction-forms-authoring.md) to know more about Adaptive Forms. -->

## 版面型別 {#types-of-layouts}

最適化表單提供下列版面型別：

**[!UICONTROL 面板配置]** 控制面板內的專案或元件在裝置上的顯示方式。

**[!UICONTROL 行動佈局]** 控制行動裝置上表單的導覽。 如果裝置寬度為768畫素或更高，此版面會被視為行動版面，並針對行動裝置進行最佳化。

**[!UICONTROL 工具列配置]** 控制動作按鈕在表單中工具列或面板工具列中的位置。

所有這些面板配置均定義於 `/libs/fd/af/layouts` 位置。

若要變更最適化表單的版面，請在以下位置使用製作模式： [!DNL Experience Manager].

## [!UICONTROL 面板布局] {#panel-layout}

表單作者可以將版面配置與最適化表單的每個面板相關聯，包括根面板。

面板配置位於 `/libs/fd/af/layouts/panel` 位置。 點選面板並選取 ![cmppr1](assets/configure-icon.svg) 以檢視面板屬性。

![最適化表單根面板的面板配置清單](assets/layouts.png)

### [!UICONTROL Responsive — 全部於單頁無需導覽] {#responsive-everything-on-one-page-without-navigation-br}

使用此面板版面配置可建立回應式版面，此版面可依裝置的熒幕大小進行調整，而不需要任何專門的導覽。

使用此版面，您可以放置多個 **[!UICONTROL 面板最適化表單]** 元件在面板中一個接一個。

![使用回應式版面的表單（如小熒幕所示）](assets/responsive-layout.png)

### [!UICONTROL 向导] {#wizard}

使用此面板版面配置在表單內提供引導式導覽。 例如，當您想要在表單中擷取必要資訊，同時逐步引導使用者時，請使用此版面。

使用 **[!UICONTROL 面板最適化表單]** 元件，在面板內提供逐步導覽。 使用此版面配置時，使用者只會在目前步驟完成後移至下一個步驟

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![使用精靈配置的表單](assets/wizard-layout2.png)

### [!UICONTROL 折叠] {#layout-for-accordion-design}

使用此版面，您可以放置 **[!UICONTROL 面板最適化表單]** 面板中的元件，具有摺疊式功能表樣式導覽。 使用此版面，您也可以建立可重複的面板。 可重複面板可讓您視需要動態新增或移除面板。 您可以定義面板重複的最小和最大次數。 此外，面板的標題可以根據面板專案中提供的資訊動態確定。

摘要運算式可用來顯示一般使用者在最小化面板標題中提供的值。

![在Adaptive Forms中使用摺疊式面板版面的可重複面板](assets/accordion-layout.png)

### [!UICONTROL 索引標籤版面配置 — 索引標籤顯示在左側 ]{#tabbed-layout-tabs-appear-on-the-left}

使用此版面，您可以放置 **[!UICONTROL 面板最適化表單]** 具有索引標籤導覽的面板中的元件。 標籤會放置在面板內容的左側。

![在「索引標籤」配置圖中，索引標籤會顯示在左側](assets/tabs-on-left.png)

出現在面板左側的索引標籤

### [!UICONTROL 索引標籤版面配置 — 索引標籤顯示在頂端] {#tabbed-layout-tabs-appear-on-the-top}

使用此版面，您可以放置 **[!UICONTROL 面板最適化表單]** 具有索引標籤導覽的面板中的元件。 索引標籤會放置在面板內容的頂端。

![最適化Forms中的索引標籤版面，頂端有索引標籤](assets/tabs-on-top.png)

## 行動版面配置 {#mobile-layouts}

行動版面配置可在熒幕較小之行動裝置上進行方便好用的導覽。 行動版面會使用索引標籤或精靈樣式來進行表單導覽。 套用行動版面配置可為整個表單提供單一版面配置。

此版面配置會使用導覽列和導覽功能表來控制導覽。 導覽列隨即顯示 **&lt;** 和 **>** 圖示表示 **[!UICONTROL 下一個]** 和 **[!UICONTROL 上一個]** 表單中的導覽步驟。

行動版面配置位於 `/libs/fd/af/layouts/mobile/` 位置。 下列行動版面預設可在Adaptive Forms中使用。

![Adaptive Forms中的行動版面清單](assets/mobile-navigation.png)

選取 **[!UICONTROL 將回應式版面的可導覽專案新增至行動功能表]** 選項以檢視適用於行動版面配置中面板的可導覽選項。 可導覽選項只有在選取 **[!UICONTROL 回應式]** 面板的配置。

使用行動版面時，可點選表單功能表來存取各種表單面板 ![aem6forms_form_menu](assets/rail-icon.svg) 圖示。

### [!UICONTROL 在表單標題中使用面板標題的佈局] {#layout-with-panel-titles-in-the-form-header}

如名稱所示，此版面會顯示面板標題以及導覽功能表和導覽列。 此版面配置也提供用於導覽的「下一個」和「上一個」圖示。

![行動版面配置在表單標題中具有面板標題](assets/mobile-layout1.png)

### [!UICONTROL 版面配置中表單標題沒有面板標題 ]{#layout-without-panel-titles-in-the-form-header}

如名稱所建議，此版面只會顯示導覽功能表和導覽列，而不會顯示面板標題。 此版面配置也提供用於導覽的「下一個」和「上一個」圖示。

![行動版面在表單標題中沒有面板標題](assets/mobile-layout2.png)

<!-- ## Toolbar layouts {#toolbar-layouts}

A Toolbar Layout controls positioning and display of any action buttons that you add to your Adaptive Forms. The layout can be added at a form level or at a panel level.

![A list of Toolbar Layouts in Adaptive Forms to control layout of buttons](assets/toolbar-layouts.png)

A list of Toolbar Layouts in Adaptive Forms

Toolbar layouts are available at `/libs/fd/af/layouts/toolbar` location. Adaptive Forms provide the following Toolbar Layouts, by default.

### [!UICONTROL Default layout for toolbar] {#default-layout-for-toolbar}

This layout is selected as the default layout when you add any action buttons in an Adaptive Form. Selecting this layout displays the same layout for both, desktop and mobile devices.

Also, you can add multiple toolbars containing action buttons configured with this layout. An action button is associated with a form control. You can configure the toolbars to be before or after a panel.

![Default view for toolbar](assets/toolbar_layout_default.png)

Default view for toolbar

### [!UICONTROL Mobile fixed layout for toolbar] {#mobile-fixed-layout-for-toolbar}

Select this layout to provide alternate layouts for desktop and mobile devices.

For the desktop layout, you can add Action buttons using some specific labels. Only one toolbar can be configured with this layout. If more than one toolbar is configured with this layout, there is an overlap for mobile devices and only one toolbar is visible. For example, you can have a toolbar at the bottom or the top of the form, or, after or before panels in the form.

For the Mobile layout, you can add action buttons using icons.

![Mobile fixed layout for toolbar](assets/toolbar_layout_mobile_fixed.png)

Mobile fixed layout for toolbar-->
