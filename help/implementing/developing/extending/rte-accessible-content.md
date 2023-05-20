---
title: 設定RTE以建立無障礙的網頁和網站。
description: 瞭解如何設定RTF編輯器，以在中建立無障礙網站 [!DNL Adobe Experience Manager].
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 配置 RTE 以创建可访问的站点 {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] 支援標準的協助工具功能，例如影像的替代文字，以及在建立內容時可存取的額外功能。 內容作者會將這些功能與使用RTF編輯器(RTE)的元件搭配使用。 功能包括新增替代文字、透過標題和段落元素的結構資訊等。

若要瞭解典型RTE設定，請參閱 [設定RTE](rich-text-editor.md) 和 [針對特定功能設定RTE外掛程式](configure-rich-text-editor-plug-ins.md).

使用RTE外掛程式設定來設定和自訂協助工具相關功能。 例如，使用 `paraformat` 以新增額外的區塊層級語意元素，包括擴充基本標題層級以外支援的標題層級數目 `H1`， `H2` 和 `H3` 預設提供。 RTF編輯可以使用編寫使用者介面的許多元件。 常用的元件有文字、影像、下載等。

RTE功能可用於許多元件。 主要元件為 `Text` 元件。

對於 `Text` 中的元件 [!DNL Experience Manager]，下列熒幕擷圖顯示已啟用多種外掛程式的RTF編輯器，包括 `paraformat`：

![全熒幕模式的RTE文字元件](assets/rte-toolbar-full-screen-mode.png)

## 設定外掛程式功能 {#configuring-the-plugin-features}

如需設定RTE的說明，請參閱 [設定RTF編輯器](rich-text-editor.md) 頁面。 文章涵蓋：

* [外掛程式及其功能](rich-text-editor.md#aboutplugins)
* [設定位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [啟動外掛程式並設定功能屬性](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [設定RTE的其他功能](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

若要針對外掛程式啟動幾項或所有功能，請在適當位置設定外掛程式 `rtePlugins` CRXDE Lite中的支行。

![顯示rtePlugin範例的CRXDE Lite](assets/example-rteplugin-crxde-lite.png)

### 指定RTE選取欄位中可用段落格式的範例 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語意區塊格式可供選取。

1. 根據您的RTE，決定並導覽至 [設定位置](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [啟用段落選擇欄位](rich-text-editor.md) 作者： [啟用外掛程式](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [在段落選取欄位中指定您想要的可用格式](rich-text-editor.md).
1. 然後，內容作者可以從RTE的選擇欄位中使用段落格式。

透過RTE中可用的段落格式選項的結構元素， [!DNL Experience Manager] 為開發無障礙內容提供了良好的基礎。 內容作者無法使用RTE來格式化字型大小、顏色或其他相關屬性，因而無法建立內嵌格式。 相反地，作者可以選取適當的結構元素（例如標題），並使用從「樣式」選項中選擇的全域樣式，以確保對於使用自己的樣式表和正確結構化的內容瀏覽的使用者來說，會有乾淨的標籤和更好的選項。

## 使用來源編輯功能 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現必須檢查和調整使用RTE建立的HTML原始碼。 例如，在RTE內建立的內容片段可能需要更多標籤，以確保符合WCAG 2.0。您可以透過以下專案完成此作業： [來源編輯](rich-text-editor.md#aboutplugins) RTE選項。 您可以指定 [`sourceedit` 上的功能 `misctools` 外掛程式](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>使用 `sourceedit` 功能精心。 任何輸入錯誤和不受支援的功能都可能導致問題。

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [WCAG標準快速指南](/help/compliance/accessibility/quick-guide-wcag.md)
>* [如何在Experience Manager中建立無障礙內容](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

