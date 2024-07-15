---
title: 配置RTE以创建可访问的网页和站点。
description: 了解如何配置富文本编辑器以在 [!DNL Adobe Experience Manager]中创建可访问的站点。
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# 配置 RTE 以创建可访问的站点 {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager]支持标准辅助功能，例如图像的替换文本以及在创建内容时可以访问的额外功能。 内容作者将这些功能与使用富文本编辑器(RTE)的组件结合使用。 这些功能包括添加替换文本、通过标题和段落元素添加结构信息等。

要了解RTE的典型配置，请参阅[配置RTE](rich-text-editor.md)和[为特定功能配置RTE插件](configure-rich-text-editor-plug-ins.md)。

使用RTE插件配置来配置和自定义与辅助功能相关的功能。 例如，使用`paraformat`添加额外的块级语义元素，包括扩展支持的标题级别数超过默认提供的基本`H1`、`H2`和`H3`。 使用创作用户界面中的许多组件，可以进行富文本编辑。 常用的组件有文本、图像、下载等。

RTE功能可以在许多组件中使用。 主要组件是`Text`组件。

对于[!DNL Experience Manager]中的`Text`组件，以下屏幕截图显示了启用了一系列插件（包括`paraformat`）的富文本编辑器：

全屏模式下的![RTE文本组件](assets/rte-toolbar-full-screen-mode.png)

## 配置插件功能 {#configuring-the-plugin-features}

有关配置RTE的说明，请参阅[配置富文本编辑器](rich-text-editor.md)页面。 本文涵盖：

* [插件及其功能](rich-text-editor.md#aboutplugins)
* [配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [激活插件并配置功能属性](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [配置RTE的其他功能](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

要为插件激活几项或所有功能，请在CRXDE Lite中相应的`rtePlugins`子分支中配置该插件。

![CRXDE Lite显示示例rtePlugin](assets/example-rteplugin-crxde-lite.png)

### 指定RTE选择字段中可用的段落格式的示例 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的语义块格式可供选择。

1. 根据您的RTE，确定并导航到[配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [通过激活插件](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)启用段落选择字段](rich-text-editor.md)。[
1. [指定您希望段落选择字段中可用的格式](rich-text-editor.md)。
1. 然后，内容作者可以从RTE中的选择字段中使用段落格式。

由于RTE中通过段落格式选项提供了结构元素，[!DNL Experience Manager]为开发无障碍内容奠定了良好的基础。 内容作者无法使用RTE设置字体大小、颜色或其他相关属性的格式，从而阻止创建内联格式。 相反，作者可以选择相应的结构元素（如标题），并使用从“样式”选项中选择的全局样式，以确保对于使用自己的样式表和正确的结构化内容浏览的用户，使用干净的标记和更多的选项。

## 使用Source编辑功能 {#use-of-the-source-edit-feature}

在某些情况下，内容作者会发现必须检查和调整使用RTE创建的HTML源代码。 例如，在RTE内创建的一段内容可能需要更多标记，以确保符合WCAG 2.0。可以使用RTE的[源编辑](rich-text-editor.md#aboutplugins)选项完成此操作。 您可以在`misctools`插件](rich-text-editor.md#aboutplugins)上指定[`sourceedit`功能。

>[!CAUTION]
>
>请仔细使用`sourceedit`功能。 任何键入错误和不受支持的功能都可能会导致问题。

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
>* [WCAG标准快速指南](/help/compliance/accessibility/quick-guide-wcag.md)
>* [如何在Experience Manager中创建可访问的内容](/help/sites-cloud/authoring/page-editor/accessible-content.md)
