---
title: 在 [!DNL Adobe Experience Manager]中配置富文本编辑器插件。
description: 了解如何配置 [!DNL Adobe Experience Manager] 富文本编辑器插件。
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '4303'
ht-degree: 2%

---

# 配置富文本编辑器插件 {#configure-the-rich-text-editor-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有功能属性。 您可以将features属性配置为启用或禁用一个或多个RTE功能。 本文介绍了如何专门配置RTE插件。

有关其他RTE配置的详细信息，请参阅[配置富文本编辑器](/help/implementing/developing/extending/rich-text-editor.md)。

>[!NOTE]
>
>在使用CRXDE Lite时，建议使用[!UICONTROL 全部保存]选项定期保存更改。

## 激活插件并配置功能属性 {#activateplugin}

要激活插件，请执行以下步骤。 只有在首次配置插件时才需要执行某些步骤，因为不存在相应的节点。

默认情况下，`format`、`link`、`list`、`justify`和`control`插件及其所有功能已在RTE中启用。

>[!NOTE]
>
>相应的`rtePlugins`节点称为`<rtePlugins-node>`，以避免本文中出现重复。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在配置任何RTE插件之前，创建`<rtePlugins-node>`的父节点（如果存在）：

   * 根据您的组件，父节点包括：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 替代配置节点： `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * 类型为： **jcr：primaryType** `cq:Widget`
   * 两者都具有以下属性：

      * **名称** `name`
      * **类型** `String`
      * **值** `./text`

1. 根据您配置的接口，创建一个节点`<rtePlugins-node>`（如果它不存在）：

   * **名称** `rtePlugins`
   * **类型** `nt:unstructured`

1. 在此路径下，为要激活的每个插件创建一个节点：

   * **类型** `nt:unstructured`
   * **名称**&#x200B;需要此插件的插件ID

激活插件后，请按照以下准则配置`features`属性。

| | 启用所有功能 | 启用一些特定功能。 | 禁用所有功能。 |
|---|---|---|---|
| 名称 | 功能 | 功能 | 功能 |
| 类型 | 字符串 | `String` (多字符串；将Type设置为`String`并单击CRXDE Lite中的`Multi`) | 字符串 |
| 价值 | `*` （星号） | 设置为一个或多个特征值。 | - |

## 了解findreplace插件 {#findreplace}

`findreplace`插件不需要任何配置。 开箱即用。

在使用替换功能时，要替换的替换字符串应与查找字符串同时输入。不过，您仍可以在替换字符串之前单击“查找”来搜索它。如果在单击“查找”后输入替换字符串，则搜索将重置到文本的开头。

在单击“查找”时，“查找和替换”对话框变为透明；在单击“替换”时，此对话框变为不透明。该行为允许作者查看要替换的文本。 如果用户单击“全部替换” ，对话框将关闭并显示所做的替换次数。

## 配置粘贴模式 {#pastemodes}

使用RTE时，作者可以通过以下三种模式之一粘贴内容：

* **浏览器模式**：使用浏览器的默认粘贴实现粘贴文本。 不建议使用此方法，因为它可能会引入不需要的标记。

* **纯文本模式**：将剪贴板内容粘贴为纯文本。 在[!DNL Experience Manager]组件中插入之前，它会从复制的内容中删除所有样式和格式元素。

* **MS Word模式**：从MS Word复制时，粘贴包含格式设置的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并且仅保留部分格式。

### 配置RTE工具栏上可用的粘贴选项  {#configure-paste-options-available-on-the-rte-toolbar}

您可以在RTE工具栏中为作者提供以下三个图标中的部分、全部或不提供：

* **[!UICONTROL 粘贴(Ctrl+V)]**：可以预配置为与上述三种粘贴模式之一相对应。

* **[!UICONTROL 粘贴为文本]**：提供纯文本模式功能。

* 从Word粘贴&#x200B;**[!UICONTROL 1&rbrace;：提供MS Word模式功能。]**

要配置RTE以显示所需的图标，请执行以下步骤。

1. 导航到您的组件，例如`/apps/<myProject>/components/text`。
1. 导航到节点`rtePlugins/edit`。 如果节点不存在，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点上创建`features`属性并添加一个或多个功能。 保存所有更改。

### 配置粘贴(Ctrl+V)图标和快捷键的行为 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

可以使用以下步骤预配置&#x200B;**[!UICONTROL 粘贴(Ctrl+V)]**&#x200B;图标的行为。 此配置还定义了作者用于粘贴内容的键盘快捷键Ctrl+V的行为。

该配置允许使用以下三种类型的用例：

* 使用浏览器的默认粘贴实施粘贴文本。 不建议使用此方法，因为它可能会引入不需要的标记。 使用下面的`browser`进行配置。

* 以纯文本形式粘贴剪贴板内容。 在[!DNL Experience Manager]组件中插入之前，它会从复制的内容中删除所有样式和格式元素。 使用下面的`plaintext`进行配置。

* 从MS Word复制时，粘贴包含格式设置的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并且仅保留部分格式。 使用下面的`wordhtml`进行配置。

1. 在组件中，导航到`<rtePlugins-node>/edit`节点。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点中，使用以下详细信息创建属性：

   * **名称** `defaultPasteMode`
   * **类型** `String`
   * **值**&#x200B;是`browser`、`plaintext`或`wordhtml`模式中所需的粘贴模式之一。

### 配置粘贴内容时允许的格式 {#pasteformats}

可以进一步配置paste-as-Microsoft-Word (`paste-wordhtml`)模式，以便在从其他程序（如[!DNL Microsoft Word]）粘贴[!DNL Experience Manager]时显式允许使用几种样式。

例如，如果在[!DNL Experience Manager]中粘贴时只允许使用粗体格式和列表，则可以筛选掉其他格式。 这称为可配置的粘贴筛选，可同时为以下两项执行该操作：

* [文本](#pastemodes)
* [链接](#linkstyles)

对于链接，您还可以定义自动接受的协议。

要配置在将文本从其他程序粘贴到[!DNL Experience Manager]时允许的格式：

1. 在组件中，导航到节点`<rtePlugins-node>/edit`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点下创建一个用于保存HTML粘贴规则的节点：

   * **名称** `htmlPasteRules`
   * **类型** `nt:unstructured`

1. 在`htmlPasteRules`下创建一个节点，以保存允许的基本格式的详细信息：

   * **名称** `allowBasics`
   * **类型** `nt:unstructured`

1. 要控制接受的各个格式，请在`allowBasics`节点上创建以下一个或多个属性：

   * **名称** `bold`
   * **名称** `italic`
   * **名称** `underline`
   * **名称** `anchor`（对于链接和命名锚点）
   * **名称** `image`

   所有属性都是&#x200B;**类型** `Boolean`，因此在适当的&#x200B;**值**&#x200B;中，您可以选择或删除复选标记以启用或禁用该功能。

   >[!NOTE]
   >
   >如果未明确定义，则使用默认值true ，并且格式可接受。

1. 也可以使用一系列其他属性或节点定义其他格式，这些属性或节点也应用于`htmlPasteRules`节点：

| 属性 | 类型 | 描述 |
|--- |--- |--- |
| `allowBlockTags` | `String` | 定义允许的块标记列表。 一些可能的块标记包括标题(h1、h2、h3)、段落(p)、列表(ol、ul)、表格(table)。 |
| `fallbackBlockTag` | `String` | 定义块标记，该标记用于具有未包含在`allowBlockTags`中的块标记的任何块。 通常，`p`就足够了。 |
| `table` | `nt:unstructured` | 定义粘贴表时的行为。 此节点必须具有属性allow（类型Boolean）才能定义是否允许粘贴表。 如果allow设置为false，则必须指定属性ignoreMode（类型String）以定义如何处理粘贴的表内容。 ignoreMode的有效值为`remove`以删除表内容，值为`paragraph`以将表单元格转换为段落。 |
| `list` | `nt:unstructured` | 定义粘贴列表时的行为。 必须具有属性`allow` （类型Boolean）以定义是否允许粘贴列表。 如果`allow`设置为`false`，请指定属性`ignoreMode` （类型`String`）以定义如何处理粘贴的任何列表内容。 ignoreMode的有效值是`remove`和`paragraph`，前者删除列表内容，后者将列表项转换为段落。 |

以下是有效`htmlPasteRules`结构的示例：

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. 保存所有更改。

## 配置文本样式 {#textstyles}

作者可以应用样式来更改部分文本的外观。 样式基于您在CSS样式表中预定义的CSS类。 使用`class`属性将样式化内容包含在`span`标记中，以引用CSS类。 例如：

`<span class=monospaced>Monospaced Text Here</span>`

首次启用样式插件时，没有默认样式可用。 弹出列表为空。 要向作者提供样式，请执行以下操作：

* 启用样式下拉选择器。
* 指定样式表的一个或多个位置。
* 指定可从样式弹出列表中选择的单个样式。

对于以后的重新配置，如要添加更多样式，请仅按照说明引用新的样式表并指定其他样式。

>[!NOTE]
>
>还可以为[表或表单元格](configure-rich-text-editor-plug-ins.md#tablestyles)定义样式。 这些配置需要单独的过程。

### 启用样式下拉选择器列表 {#styleselectorlist}

启用样式插件可完成此操作。

1. 在组件中，导航到节点`<rtePlugins-node>/styles`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`styles`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

1. 保存所有更改。

>[!NOTE]
>
>启用样式插件后，“样式”下拉列表将显示在“编辑”对话框中。 但是，列表为空，因为未配置样式。

### 指定样式表位置 {#locationofstylesheet}

然后，指定要引用的样式表的位置：

1. 导航到文本组件的根节点，例如`/apps/<myProject>/components/text`。
1. 将属性`externalStyleSheets`添加到`<rtePlugins-node>`的父节点：

   * **名称** `externalStyleSheets`
   * **Type** `String[]` （多字符串；单击CRXDE中的&#x200B;**Multi**）
   * **值**&#x200B;要包含的每个样式表的路径和文件名。 使用存储库路径。

   >[!NOTE]
   >
   >以后可随时向其它样式表添加参照。

1. 保存所有更改。

在对话框（经典UI）中使用RTE时，您可以指定针对富文本编辑优化的样式表。 由于技术限制，编辑器中的CSS上下文丢失，因此您可以模拟此上下文以改进WYSIWYG体验。

富文本编辑器使用ID为`CQrte`的容器DOM元素，该元素提供不同的样式以供查看和编辑：

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### 在弹出列表中指定可用的样式 {#stylesindropdown}

1. 在组件定义中，导航到节点`<rtePlugins-node>/styles`，如[启用样式下拉选择器](#styleselectorlist)中所创建。
1. 在节点`styles`下，创建一个节点（也称为`styles`）来保存正在提供的列表：

   * **名称** `styles`
   * **类型** `cq:WidgetCollection`

1. 在`styles`节点下创建一个节点以表示单个样式：

   * **名称**，您可以指定名称，但它应该适合样式
   * **类型** `nt:unstructured`

1. 将属性`cssName`添加到此节点以引用CSS类：

   * **名称** `cssName`
   * **类型** `String`
   * **值** CSS类的名称(不带前缀“。”；例如，`cssClass`而不是`.cssClass`)

1. 将属性`text`添加到同一节点；这将定义选择框中显示的文本：

   * **名称** `text`
   * **类型** `String`
   * **值**&#x200B;样式的描述；显示在“样式”下拉选择框中。

1. 保存更改。

   对每个所需的样式重复上述步骤。

### 配置RTE以优化日语断字 {#jpwordwrap}

使用[!DNL Experience Manager]创作日语内容的作者可以将样式应用于字符以避免不需要换行符的字符。 这允许作者在所需位置处断句。 此功能的样式基于CSS样式表中预定义的CSS类。

要创建作者可以应用于日语文本的样式，请执行以下步骤：

1. 在“样式”节点下创建一个节点。 请参阅[指定样式](#stylesindropdown)。
   * 名称：`jpn-word-wrap`
   * 类型：`nt:unstructure`

1. 将属性`cssName`添加到节点以引用CSS类。 此类名称是日语自动换行功能的保留名称。
   * 名称：`cssName`
   * 类型：`String`
   * 值： `jpn-word-wrap` （没有前一个`.`）

1. 将属性文本添加到同一节点。 值是作者在选择样式时看到的样式名称。
   * 名称： `text`
*类型： `String`
   * 值： `Japanese word-wrap`

1. 创建样式表并指定其路径。 请参阅[指定样式表](#locationofstylesheet)的位置。 将以下内容添加到样式表中。 根据需要更改背景颜色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![样式表使日文自动换行功能可供作者使用](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式 {#paraformats}

在RTE中创作的任何文本都放置在块标记中，默认值为`<p>`。 通过启用`paraformat`插件，您可以使用下拉选择列表指定可分配给段落的其他块标记。 段落格式通过指定正确的块标记来确定段落类型。 作者可以使用“格式”选择器选择和分配格式。 示例块标记包括标准段落&lt;p>和标题&lt;h1>、&lt;h2>等。

>[!CAUTION]
>
>此插件不适用于结构复杂的内容，例如列表或表。

>[!NOTE]
>
>如果无法将块标记（例如`<hr>`标记）分配给段落，则它不是`paraformat`插件的有效用例。

首次启用段落格式插件时，没有默认的段落格式可用。 弹出列表为空。 要向作者提供段落格式，请执行以下操作：

* 启用[!UICONTROL 格式]弹出选择器列表。
* 指定可从弹出菜单中选择为段落格式的块标记。

对于以后的重新配置（如要添加更多格式），请仅按照说明的相关部分操作。

### 启用格式下拉选择器 {#formatselectorlist}

要启用`paraformat`插件，请执行以下步骤：

1. 在组件中，导航到节点`<rtePlugins-node>/paraformat`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`paraformat`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

>[!NOTE]
>
>如果未进一步配置此插件，则启用的默认格式为段落( `<p>`)、标题1 (`<h1>`)、标题2 (`<h2>`)、标题3 (`<h3>`)。

>[!CAUTION]
>
>配置RTE的段落格式时，请勿删除段落标记&lt;p>作为格式设置选项。 如果移除`<p>`标记，那么即使配置了其他格式，内容作者也无法选择[!UICONTROL 段落格式]选项。

### 指定可用的段落格式 {#paraformatsindropdown}

可通过以下方式选择段落格式：

1. 在组件定义中，导航到节点`<rtePlugins-node>/paraformat`，如[启用格式下拉选择器](#styleselectorlist)中所创建。
1. 在`paraformat`节点下创建一个节点，以保存格式列表：

   * **名称** `formats`
   * **类型** `cq:WidgetCollection`

1. 在`formats`节点下创建一个节点，这将保存单个格式的详细信息：

   * **名称**，您可以指定名称，但它应该适合格式（例如，myparagraph、myheading1）。
   * **类型** `nt:unstructured`

1. 在此节点中，添加属性以定义使用的块标记：

   * **名称** `tag`
   * **类型** `String`
   * **值**&#x200B;格式的块标记；例如：p、h1、h2等。

     您无需输入分隔尖括号。

1. 要添加到同一节点，请添加另一个属性，以便在下拉列表中显示描述性文本：

   * **名称** `description`
   * **类型** `String`
   * **值**&#x200B;此格式的描述性文本；例如，段落、标题1、标题2等。 此文本显示在“格式”选择列表中。

1. 保存更改。

   对每个所需的格式重复这些步骤。

>[!CAUTION]
>
>如果您定义自定义格式，则将删除默认格式（`<p>`、`<h1>`、`<h2>`和`<h3>`）。 重新创建`<p>`格式，因为它是默认格式。

## 配置特殊字符 {#spchar}

在标准[!DNL Experience Manager]安装中，如果为特殊字符(`specialchars`)启用了`misctools`插件，则默认选择将立即可用；例如，版权和商标符号。

您可以配置RTE以使您选择的字符可用；通过定义不同的字符或整个序列。

>[!CAUTION]
>
>添加特殊字符将覆盖默认选项。 如有必要，请在所选内容中重新定义这些字符。

### 定义单个字符 {#definesinglechar}

1. 在组件中，导航到节点`<rtePlugins-node>/misctools`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`misctools`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String[]`
   * **值** `specialchars`

         (或者`String / *`（如果为此插件应用了所有功能）

1. 在`misctools`下创建一个节点以保存特殊字符配置：

   * **名称** `specialCharsConfig`
   * **类型** `nt:unstructured`

1. 在`specialCharsConfig`下创建另一个节点以保存字符列表：

   * **名称** `chars`
   * **类型** `nt:unstructured`

1. 在`chars`下添加一个节点以保存单个字符定义：

   * **名称**&#x200B;您可以指定名称，但应反映该字符；例如，一半。
   * **类型** `nt:unstructured`

1. 要添加到此节点，请添加以下属性：

   * **名称** `entity`
   * **类型** `String`
   * **值**&#x200B;所需字符的HTML表示形式；例如，`&189;`表示小数的一半。

1. 保存更改。

在CRXDE中，保存属性后，将显示表示的字符。 请参阅下面的示例中一半内容。 重复以上步骤以使作者可以使用更多特殊字符。

![在CRXDE中，添加一个可在RTE工具栏中使用的字符](assets/chlimage_1-106.png "在CRXDE中，添加一个可在RTE工具栏中使用的字符")

### 定义字符范围 {#definerangechar}

1. 使用[中的步骤1至3定义单个字符](#definesinglechar)。
1. 在`chars`下添加一个节点以保存字符范围的定义：

   * **名称**&#x200B;您可以指定名称，但它应反映字符范围；例如，铅笔。
   * **类型** `nt:unstructured`

1. 在此节点下（根据特殊字符范围命名）添加以下两个属性：

   * **名称** `rangeStart`

     **类型** `Long`
     **值**&#x200B;范围中第一个字符的[Unicode](https://unicode.org/)表示形式（十进制）

   * **名称** `rangeEnd`

     **类型** `Long`
     **值**&#x200B;范围中最后一个字符的[Unicode](https://unicode.org/)表示形式（十进制）

1. 保存更改。

   例如，定义9998到10000之间的范围时，为您提供了以下字符。

   ![在CRXDE中，定义在RTE中可用的字符范围](assets/chlimage_1-107.png)

   *图：在CRXDE中，定义在RTE*&#x200B;中可用的字符范围

   ![在弹出窗口中向作者显示RTE中可用的特殊字符](assets/rtepencil.png "在弹出窗口中向作者显示RTE中可用的特殊字符")

## 配置表样式 {#tablestyles}

样式通常应用于文本，但也可以对表或几个表单元格应用单独的样式集。 作者可以在“单元格属性”或“表属性”对话框的“样式选择器”框中找到此类样式。 在文本组件（或派生项）中编辑表时样式可用，在标准表组件中则不可用。

>[!NOTE]
>
>您只能为经典UI定义表和单元格的样式。

>[!NOTE]
>
>在RTE组件中或从RTE组件中复制和粘贴表依赖于浏览器。 并非所有浏览器都支持开箱即用。 根据表结构和浏览器，可能会得到不同的结果。 例如，在经典UI和触屏UI中，当您在Mozilla Firefox的RTE组件中复制并粘贴表时，不会保留表的布局。

1. 在您的组件中，导航到节点`<rtePlugins-node>/table`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`table`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*`

   >[!NOTE]
   >
   >如果不希望启用所有表功能，您可以创建`features`属性，如下所示：
   >
   >* **类型** `String[]`
   >
   >* **值**（根据需要）以下一项或两项：
   >* `table`以允许编辑表属性；包括样式。
   >* `cellprops`以允许编辑单元格属性，包括样式。

1. 定义CSS样式表的位置以引用这些样式表。 请参阅[指定样式表](#locationofstylesheet)的位置，因为这与为文本定义[样式](#textstyles)的位置相同。 如果定义了其他样式，则可以定义位置。
1. 在`table`节点下，根据需要创建以下节点：

   * 要为整个表定义样式（可在&#x200B;**[!UICONTROL 表属性]**&#x200B;下使用）：

      * **名称** `tableStyles`
      * **类型** `cq:WidgetCollection`

   * 要为单个单元格定义样式（可在&#x200B;**[!UICONTROL 单元格属性]**&#x200B;下使用），请执行以下操作：

      * **名称** `cellStyles`
      * **类型** `cq:WidgetCollection`

1. 创建一个节点（视情况在`tableStyles`或`cellStyles`节点下）以表示单个样式，

   * **名称**&#x200B;您可以指定名称，但它应反映样式。
   * **类型** `nt:unstructured`

1. 在此节点上创建属性：

   * 要定义引用的CSS样式，

      * **名称** `cssName`
      * **类型** `String`
      * **值** CSS类的名称（不带前缀`.`，例如`cssClass`而不是`.cssClass`）

   * 要定义要在弹出式选择器中显示的描述性文本，请执行以下操作：

      * **名称** `text`
      * **类型** `String`
      * **值**&#x200B;要显示在选择列表中的文本

1. 保存所有更改。

对每个所需的样式重复上述步骤。

### 为辅助功能配置表中的隐藏标头 {#hiddenheader}

有时，您可以创建没有可视文本的数据表，但前提是列标题的用途隐含在列与其他列的视觉关系中。 在这种情况下，有必要在标题单元格的单元格中提供隐藏的内部文本，以允许屏幕阅读器和其他辅助技术帮助有各种需求的阅读器了解列的用途。

为了在这种情况下增强辅助功能，RTE支持隐藏的标题单元格。 此外，它还提供与表中隐藏标头相关的配置设置。 这些设置允许您在编辑和预览模式下对隐藏的标题应用CSS样式。 为帮助作者在编辑模式下识别隐藏的标头，请在代码中包含以下参数：

* `hiddenHeaderEditingCSS`：指定编辑RTE时应用于hidden-header单元格的CSS类的名称。
* `hiddenHeaderEditingStyle`：指定编辑RTE时应用于hidden-header单元格的Style字符串。

如果在代码中同时指定CSS和Style字符串，则CSS类将优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

为帮助作者在预览模式下对隐藏的标题应用CSS，您可以在代码中包含以下参数：

* `hiddenHeaderClassName`：指定在预览模式下应用于隐藏标题单元格的CSS类的名称。
* `hiddenHeaderStyle`：指定在预览模式下应用于hidden-header单元格的样式字符串。

如果在代码中同时指定CSS和Style字符串，则CSS类将优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

## 为拼写检查器添加词典 {#adddict}

当激活spellcheck插件时，RTE会为每种相应的语言使用词典。 然后，通过获取子树的语言属性或者从URL中提取语言来根据网站的语言选择这些语言；例如。 `/en/`分支被检查为英文，`/de/`分支被检查为德文。

>[!NOTE]
>
>消息“拼写检查失败。” 如果尝试检查未安装的语言，则会显示。

标准Experience Manager安装包括以下词典：

* 美国英语(en_us)
* 英式英语(en_gb)

>[!NOTE]
>
>标准字典位于`/libs/cq/spellchecker/dictionaries`，以及相应的自述文件。 请勿修改文件。

要添加更多词典，请按照以下步骤操作（如有必要）。

1. 导航到页面[https://extensions.openoffice.org/](https://extensions.openoffice.org/)。
1. 选择所需的语言并下载包含拼写定义的ZIP文件。 提取文件系统中存档文件的内容。

   >[!CAUTION]
   >
   >仅支持OpenOffice.org v2.0.1或更低版本中采用`MySpell`格式的词典。 由于字典现在是存档文件，因此建议您在下载后验证存档。

1. 找到.aff和.dic文件。 请将文件名保留为小写。 例如，`de_de.aff`和`de_de.dic`。
1. 在`/apps/cq/spellchecker/dictionaries`处的存储库中加载.aff和.dic文件。

>[!NOTE]
>
>RTE拼写检查器可按需使用。 当您开始键入文本时，它不会自动运行。
>
>要运行拼写检查器，请从工具栏中选择拼写检查器按钮。 RTE检查单词的拼写并突出显示拼写错误的单词。
>
>如果合并拼写检查器建议的任何更改，则文本的状态将发生更改，拼写错误的单词将不再突出显示。 要运行拼写检查器，请再次选择“拼写检查器”按钮。

## 配置撤消和重做操作的历史记录大小 {#undohistory}

RTE允许作者撤消或重做前几次编辑。 默认情况下，历史中存储50次编辑。 您可以根据需要配置此值。

1. 在您的组件中，导航到节点`<rtePlugins-node>/undo`。 创建这些节点（如果这些节点不存在）。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`undo`节点上创建属性：

   * **名称** `maxUndoSteps`
   * **类型** `Long`
   * **值**&#x200B;要保存在历史记录中的撤消步骤数。 默认值为50。 使用`0`可完全禁用撤消/重做。

1. 保存更改。

## 配置选项卡大小 {#tabsize}

当在任意文本中按制表符字符时，会插入预定义的空格数；默认情况下，这是三个不间断的空格和一个空格。

要定义选项卡大小，请执行以下操作：

1. 在组件中，导航到节点`<rtePlugins-node>/keys`。 如果节点不存在，则创建节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`keys`节点上创建属性：

   * **名称** `tabSize`
   * **类型** `String`
   * **值**&#x200B;用于制表器的空格字符数。

1. 保存更改。

## 设置缩进边距 {#indentmargin}

启用缩进（默认）后，您可以定义缩进的大小：

>[!NOTE]
>
>此缩进大小仅适用于文本的段落（块）；它不会影响实际列表的缩进。

1. 在您的组件中，导航到节点`<rtePlugins-node>/lists`。 创建这些节点（如果这些节点不存在）。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`lists`节点上创建`identSize`参数：

   * **名称**：`identSize`
   * **类型**：`Long`
   * **值**：缩进边距所需的像素数。

## 配置可编辑空间的高度 {#editablespace}

您可以定义在组件对话框中显示的可编辑空间的高度。 仅当在对话框中使用RTE时，配置才适用。 配置不会更改对话框窗口的高度。

1. 在`../items/text`节点中，在组件的对话框定义中创建属性：

   * **名称** `height`
   * **类型** `Long`
   * **值**&#x200B;编辑画布的高度（像素）。

1. 保存更改。

## 为链接配置样式和协议 {#linkstyles}

在[!DNL Experience Manager]中添加链接时，您可以定义要使用的CSS样式以及要自动接受的协议。 要配置链接如何从其他程序添加到[!DNL Experience Manager]中，请定义HTML规则。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在与`<rtePlugins-node>`相同的级别上创建一个节点，即在`<rtePlugins-node>`的父节点下创建该节点：

   * **名称** `htmlRules`
   * **类型** `nt:unstructured`

   >[!NOTE]
   >
   >`../items/text`节点具有属性：
   >
   >* **名称** `xtype`
   >* **类型** `String`
   >* **值** `richtext`
   >
   >`../items/text`节点的位置可能因对话框的结构而异。 两个示例是`/apps/myProject>/components/text/dialog/items/text`和`/apps/<myProject>/components/text/dialog/items/panel/items/text`。

1. 在`htmlRules`下，创建一个节点。

   * **名称** `links`
   * **类型** `nt:unstructured`

1. 在`links`节点下，根据需要定义属性：

   * 内部链接的CSS样式：

      * **名称** `cssInternal`
      * **类型** `String`
      * **值** CSS类的名称(不带前缀“。”；例如，`cssClass`而不是`.cssClass`)

   * 外部链接的CSS样式

      * **名称** `cssExternal`
      * **类型** `String`
      * **值** CSS类的名称(不带前缀“。”；例如，`cssClass`而不是`.cssClass`)

   * 有效&#x200B;**[!UICONTROL 协议]**&#x200B;的数组，包括`https://`、`https://`、`file://`、`mailto:`等，

      * **名称** `protocols`
      * **类型** `String[]`
      * **值**&#x200B;一个或多个协议

   * **defaultProtocol** （类型为&#x200B;**字符串**&#x200B;的属性）：用户未明确指定协议时要使用的协议。

      * **名称** `defaultProtocol`
      * **类型** `String`
      * **值**&#x200B;一个或多个默认协议

   * 有关如何处理链接的目标属性的定义。 创建节点：

      * **名称** `targetConfig`
      * **类型** `nt:unstructured`

     在节点`targetConfig`上：定义所需的属性：

      * 指定目标模式：

         * **名称** `mode`
         * **类型** `String`)
         * **值**：

            * `auto`：表示选择了自动目标

              （由外部链接的`targetExternal`属性或内部链接的`targetInternal`指定）。

            * `manual`：在此上下文中不适用
            * `blank`：在此上下文中不适用

      * 内部链接的目标：

         * **名称** `targetInternal`
         * **类型** `String`
         * **值**&#x200B;内部链接的目标（仅在模式为`auto`时使用）

      * 外部链接的目标：

         * **名称** `targetExternal`
         * **类型** `String`
         * **值**&#x200B;外部链接的目标（仅在模式为`auto`时使用）。

1. 保存所有更改。
