---
title: 在中配置富文本编辑器插件 [!DNL Adobe Experience Manager].
description: 了解如何配置 [!DNL Adobe Experience Manager] 富文本编辑器插件。
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 4%

---

# 配置富文本编辑器插件 {#configure-the-rich-text-editor-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有features属性。 您可以配置一个或多个RTE功能，以启用或禁用该功能属性。 本文介绍了如何具体配置RTE插件。

有关其他RTE配置的详细信息，请参阅 [配置富文本编辑器](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>使用CRXDE Lite时，建议使用 [!UICONTROL 全部保存] 选项。

## 激活插件并配置功能属性 {#activateplugin}

要激活插件，请执行以下步骤。 仅当您首次配置插件时，才需要执行某些步骤，因为相应的节点不存在。

默认情况下， `format`, `link`, `list`, `justify`和 `control` 插件及其所有功能均已在RTE中启用。

>[!NOTE]
>
>相应 `rtePlugins` 节点称为 `<rtePlugins-node>` 以避免在本文中出现重复。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 创建的父节点 `<rtePlugins-node>` 如果不存在，则在配置任何RTE插件之前：

   * 根据您的组件，父节点包括：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 备用配置节点： `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 类型为： **jcr:primaryType** `cq:Widget`
   * 这两者都具有以下属性：

      * **名称** `name`
      * **类型** `String`
      * **值** `./text`


1. 根据您配置的界面，创建节点 `<rtePlugins-node>`，如果不存在：

   * **名称** `rtePlugins`
   * **类型** `nt:unstructured`

1. 在下面，为要激活的每个插件创建一个节点：

   * **类型** `nt:unstructured`
   * **名称** 所需插件的插件ID

激活插件后，请按照以下准则配置 `features` 属性。

|  | 启用所有功能 | 启用一些特定功能。 | 禁用所有功能。 |
|---|---|---|---|
| 名称 | 功能 | 功能 | 功能 |
| 类型 | 字符串 | `String` (多字符串；将类型设置为 `String` 单击 `Multi` CRXDE Lite) | 字符串 |
| 值 | `*` （星号） | 设置为一个或多个特征值。 | - |

## 了解findreplace插件 {#findreplace}

的 `findreplace` 插件不需要任何配置。 它开箱即用。

在使用替换功能时，要替换的替换字符串应与查找字符串同时输入。不过，您仍可以在替换字符串之前单击“查找”来搜索它。如果在单击“查找”后输入替换字符串，则搜索将重置到文本的开头。

在单击“查找”时，“查找和替换”对话框变为透明；在单击“替换”时，此对话框变为不透明。行为允许作者查看要替换的文本。 如果用户单击“全部替换”，则对话框将关闭并显示已进行替换的数量。

## 配置粘贴模式 {#pastemodes}

使用RTE时，作者可以以以下三种模式之一粘贴内容：

* **浏览器模式**:使用浏览器的默认粘贴实施粘贴文本。 它不是推荐的方法，因为它可能会引入不需要的标记。

* **纯文本模式**:将剪贴板内容粘贴为纯文本。 在插入之前，它会删除复制内容中的所有样式和格式元素 [!DNL Experience Manager] 组件。

* **MS Word模式**:从MS Word复制时，粘贴带格式的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并仅保留部分格式。

### 配置RTE工具栏上的粘贴选项  {#configure-paste-options-available-on-the-rte-toolbar}

在RTE工具栏中，您可以为作者提供以下三个图标中的一些、全部或无一个：

* **[!UICONTROL 粘贴(Ctrl+V)]**:可以预配置为与上述三种粘贴模式之一对应。

* **[!UICONTROL 粘贴为文本]**:提供纯文本模式功能。

* **[!UICONTROL 从Word粘贴]**:提供MS Word模式功能。

要配置RTE以显示所需的图标，请执行以下步骤。

1. 导航到您的组件，例如 `/apps/<myProject>/components/text`.
1. 导航到节点 `rtePlugins/edit`. 请参阅 [激活插件](#activateplugin) 如果节点不存在。
1. 创建 `features` 属性 `edit` 节点，并添加一个或多个功能。 保存所有更改。

### 配置“粘贴”(Ctrl+V)图标和快捷键的行为 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

您可以预配置 **[!UICONTROL 粘贴(Ctrl+V)]** 图标。 此配置还定义作者用于粘贴内容的键盘快捷键Ctrl+V的行为。

配置允许使用以下三种类型的用例：

* 使用浏览器的默认粘贴实施粘贴文本。 它不是推荐的方法，因为它可能会引入不需要的标记。 使用 `browser` 下。

* 将剪贴板内容粘贴为纯文本。 在插入之前，它会删除复制内容中的所有样式和格式元素 [!DNL Experience Manager] 组件。 使用 `plaintext` 下。

* 从MS Word复制时，粘贴带格式的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并仅保留部分格式。 使用 `wordhtml` 下。

1. 在您的组件中，导航到 `<rtePlugins-node>/edit` 节点。 如果节点不存在，则创建节点。 有关更多信息，请参阅 [激活插件](#activateplugin).
1. 在 `edit` 节点使用以下详细信息创建属性：

   * **名称** `defaultPasteMode`
   * **类型** `String`
   * **值** 是 `browser`, `plaintext`或 `wordhtml` 模式。

### 配置粘贴内容时允许的格式 {#pasteformats}

粘贴为Microsoft字(`paste-wordhtml`)模式，以便您能够在粘贴时明确允许使用一些样式 [!DNL Experience Manager] 来自其他项目，例如 [!DNL Microsoft Word].

例如，如果在粘贴时仅允许使用粗体格式和列表 [!DNL Experience Manager]，则可以过滤掉其他格式。 这称为可配置粘贴过滤，可用于以下两项：

* [文本](#pastemodes)
* [链接](#linkstyles)

对于链接，您还可以定义自动接受的协议。

配置将文本粘贴到中时允许使用的格式 [!DNL Experience Manager] 从另一个程序中：

1. 在您的组件中，导航到节点 `<rtePlugins-node>/edit`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `edit` 用于保存HTML粘贴规则的节点：

   * **名称** `htmlPasteRules`
   * **类型** `nt:unstructured`

1. 在下创建节点 `htmlPasteRules`，以保存所允许的基本格式的详细信息：

   * **名称** `allowBasics`
   * **类型** `nt:unstructured`

1. 要控制接受的各个格式，请在 `allowBasics` 节点：

   * **名称** `bold`
   * **名称** `italic`
   * **名称** `underline`
   * **名称** `anchor` （对于链接和命名锚点）
   * **名称** `image`

   所有属性均为 **类型** `Boolean`，因此在适当的 **值** 您可以选择或删除复选标记以启用或禁用功能。

   >[!NOTE]
   >
   >如果未明确定义，则使用默认值true，并接受格式。

1. 也可以使用一系列其他属性或节点来定义其他格式，这些属性或节点也应用于 `htmlPasteRules` 节点：

| 属性 | 类型 | 描述 |
|--- |--- |--- |
| `allowBlockTags` | `String` | 定义允许的块标记列表。 一些可能的块标记包括标题(h1、h2、h3)、段落(p)、列表(ol、ul)、表(table)。 |
| `fallbackBlockTag` | `String` | 定义块标记，该标记用于任何块中未包含块标记 `allowBlockTags`. 通常， `p` 够了。 |
| `table` | `nt:unstructured` | 定义粘贴表时的行为。 此节点必须具有属性allow（类型Boolean）来定义是否允许粘贴表。 如果将allow设置为false，则必须指定属性ignoreMode（类型字符串）以定义如何处理粘贴的表内容。 ignoreMode的有效值为 `remove` 删除表内容和 `paragraph` 将表格单元格转换为段落。 |
| `list` | `nt:unstructured` | 定义粘贴列表时的行为。 必须具有资产 `allow` （类型布尔值）来定义是否允许粘贴列表。 如果 `allow` 设置为 `false`，指定属性 `ignoreMode` （类型） `String`)以定义如何处理粘贴的任何列表内容。 ignoreMode的有效值为 `remove` 删除列表内容和 `paragraph` 可将列表项转换为段落。 |

有效的示例 `htmlPasteRules` 结构如下：

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

作者可以应用样式来更改部分文本的外观。 样式基于您在CSS样式表中预定义的CSS类。 风格化内容包含在 `span` 标记使用 `class` 属性引用CSS类。 例如：

`<span class=monospaced>Monospaced Text Here</span>`

首次启用“样式”插件后，没有可用的默认样式。 弹出列表为空。 要为作者提供样式，请执行以下操作：

* 启用样式下拉选择器。
* 指定样式表的一个或多个位置。
* 指定可从样式弹出列表中选择的各个样式。

要稍后进行重新配置，请假设要添加更多样式，请仅按照说明引用新样式表并指定其他样式。

>[!NOTE]
>
>还可以为 [表或表单元格](configure-rich-text-editor-plug-ins.md#tablestyles). 这些配置需要单独的过程。

### 启用样式下拉选择器列表 {#styleselectorlist}

这是通过启用样式插件来完成的。

1. 在您的组件中，导航到节点 `<rtePlugins-node>/styles`. 如果节点不存在，则创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 属性 `styles` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

1. 保存所有更改。

>[!NOTE]
>
>启用“样式”插件后，“样式”下拉列表将显示在编辑对话框中。 但是，该列表为空，因为未配置样式。

### 指定样式表位置 {#locationofstylesheet}

然后，指定要引用的样式表的位置：

1. 导航到文本组件的根节点，例如 `/apps/<myProject>/components/text`.
1. 添加属性 `externalStyleSheets` 的父节点 `<rtePlugins-node>`:

   * **名称** `externalStyleSheets`
   * **类型** `String[]` (多字符串；单击 **多** （在CRXDE中）
   * **值** 要包含的每个样式表的路径和文件名。 使用存储库路径。

   >[!NOTE]
   >
   >您可以在以后任何时间添加对其他样式表的引用。

1. 保存所有更改。

在对话框中使用RTE（经典UI）时，可以指定针对富文本编辑而优化的样式表。 由于技术限制，编辑器中会丢失CSS上下文，因此您可以模拟此上下文以改进所见即所得(WYSIWYG)体验。

富文本编辑器使用ID为的容器DOM元素 `CQrte` 提供了不同样式以进行查看和编辑：

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

1. 在组件定义中，导航到节点 `<rtePlugins-node>/styles`，在中创建 [启用样式下拉选择器](#styleselectorlist).
1. 在节点下 `styles`，创建节点(也称为 `styles`)以保存正在提供的列表：

   * **名称** `styles`
   * **类型** `cq:WidgetCollection`

1. 在 `styles` 表示单个样式的节点：

   * **名称**，您可以指定名称，但该名称应适合样式
   * **类型** `nt:unstructured`

1. 添加属性 `cssName` 到此节点以引用CSS类：

   * **名称** `cssName`
   * **类型** `String`
   * **值** CSS类的名称（不带前面的“。”）;例如， `cssClass` 而不是 `.cssClass`)

1. 添加属性 `text` 到同一节点；这定义了选择框中显示的文本：

   * **名称** `text`
   * **类型** `String`
   * **值** 风格描述；显示在“样式”下拉选择框中。

1. 保存更改。

   对每个必需的样式重复上述步骤。

### 配置RTE以获取最佳日语分词 {#jpwordwrap}

使用 [!DNL Experience Manager] 要创作日语内容，可以对字符应用样式以避免不需要中断的换行符。 这允许作者让句子在所需位置中断。 此功能的样式基于在CSS样式表中预定义的CSS类。

要创建作者可以应用于日语文本的样式，请执行以下步骤：

1. 在“样式”节点下创建一个节点。 请参阅 [指定样式](#stylesindropdown).
   * 名称: `jpn-word-wrap`
   * 类型: `nt:unstructure`

1. 添加属性 `cssName` 引用CSS类的节点。 此类名称是日语自动换行功能的保留名称。
   * 名称: `cssName`
   * 类型: `String`
   * 值： `jpn-word-wrap` (没有前面的 `.`)

1. 将属性文本添加到同一节点。 值是作者选择样式时看到的样式名称。
   * 名称： `text`
*类型： 
`String`
   * 值: `Japanese word-wrap`

1. 创建样式表并指定其路径。 请参阅 [指定样式表的位置](#locationofstylesheet). 将以下内容添加到样式表。 根据需要更改背景颜色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![用于向作者提供日语文字换行功能的样式表](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式 {#paraformats}

在RTE中创作的任何文本都放置在块标记中，默认为 `<p>`. 通过启用 `paraformat` 插件中，您可以使用下拉选择列表指定可分配给段落的其他块标记。 段落格式通过分配正确的块标记来确定段落类型。 作者可以使用格式选择器选择和分配它们。 示例块标记包括标准段落 &lt;p> 和标题 &lt;h1>, &lt;h2>，等等。

>[!CAUTION]
>
>此插件不适用于结构复杂的内容，如列表或表。

>[!NOTE]
>
>如果块标记，例如 `<hr>` 标记，无法将其分配给段落，因此它不是 `paraformat` 插件。

首次启用“段落格式”插件后，不提供默认的“段落格式”。 弹出列表为空。 要为作者提供段落格式，请执行以下操作：

* 启用 [!UICONTROL 格式] 弹出选择器列表。
* 指定可从弹出菜单中选择为段落格式的块标记。

有关以后的重新配置，例如要添加更多格式，请仅按照说明的相关部分操作。

### 启用“格式”下拉选择器 {#formatselectorlist}

启用 `paraformat` 插件，请按照以下步骤操作：

1. 在您的组件中，导航到节点 `<rtePlugins-node>/paraformat`. 如果节点不存在，则创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 属性 `paraformat` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

>[!NOTE]
>
>如果未进一步配置插件，则启用的默认格式为“段落”( `<p>`)，标题1( `<h1>`)，标题2( `<h2>`)，标题3( `<h3>`)。

>[!CAUTION]
>
>配置RTE的段落格式时，请勿删除段落标记 &lt;p> 作为格式选项。 如果 `<p>` 标记被删除，内容作者将无法选择 [!UICONTROL 段落格式] 选项。

### 指定可用的段落格式 {#paraformatsindropdown}

段落格式可通过以下方式进行选择：

1. 在组件定义中，导航到节点 `<rtePlugins-node>/paraformat`，在中创建 [启用格式下拉选择器](#styleselectorlist).
1. 在 `paraformat` 节点创建节点，以保存格式列表：

   * **名称** `formats`
   * **类型** `cq:WidgetCollection`

1. 在 `formats` 节点中，它保存单个格式的详细信息：

   * **名称**，您可以指定名称，但该名称应适用于格式（例如，myparagraph、myheading1）。
   * **类型** `nt:unstructured`

1. 对于此节点，添加属性以定义使用的块标记：

   * **名称** `tag`
   * **类型** `String`
   * **值** 格式的块标记；例如：p、h1、h2等

      您无需输入分隔尖括号。

1. 对于同一节点，添加另一个属性，以便描述性文本显示在下拉列表中：

   * **名称** `description`
   * **类型** `String`
   * **值** 此格式的描述性文本；例如，段落、标题1、标题2，等等。 此文本显示在“格式”选择列表中。

1. 保存更改。

   对每种所需的格式重复这些步骤。

>[!CAUTION]
如果定义自定义格式，则默认格式(`<p>`, `<h1>`, `<h2>`和 `<h3>`)。 重新创建 `<p>` 格式，因为它是默认格式。

## 配置特殊字符 {#spchar}

标准 [!DNL Experience Manager] 安装时 `misctools` 插件适用于特殊字符(`specialchars`)默认选项可立即使用；例如，版权和商标符号。

可以配置RTE以使选择的字符可用；通过定义不同的字符或整个序列。

>[!CAUTION]
添加特殊字符将覆盖默认选择。 如果需要，在选择中重定义这些字符。

### 定义单个字符 {#definesinglechar}

1. 在您的组件中，导航到节点 `<rtePlugins-node>/misctools`. 如果节点不存在，则创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 属性 `misctools` 节点：

   * **名称** `features`
   * **类型** `String[]`
   * **值** `specialchars`

          (或 `String / *` 如果为此插件应用所有功能，则

1. 在 `misctools` 创建用于保存特殊字符配置的节点：

   * **名称** `specialCharsConfig`
   * **类型** `nt:unstructured`

1. 在 `specialCharsConfig` 创建另一个节点以保存字符列表：

   * **名称** `chars`
   * **类型** `nt:unstructured`

1. 在 `chars` 添加节点以保存单个字符定义：

   * **名称** 可以指定名称，但应反映字符；例如，一半。
   * **类型** `nt:unstructured`

1. 向此节点添加以下属性：

   * **名称** `entity`
   * **类型** `String`
   * **值** 所需字符的HTML表示；例如， `&189;` 半份。

1. 保存更改。

在CRXDE中，保存属性后，即会显示表示的字符。 请参阅下面的“一半”示例。 重复上述步骤，为作者提供更多特殊字符。

![在CRXDE中，添加一个要在RTE工具栏中提供的字符](assets/chlimage_1-106.png "在CRXDE中，添加一个要在RTE工具栏中提供的字符")

### 定义字符范围 {#definerangechar}

1. 使用 [定义单个字符](#definesinglechar).
1. 在 `chars` 添加用于保存字符范围定义的节点：

   * **名称** 可以指定名称，但应反映字符范围；例如，铅笔。
   * **类型** `nt:unstructured`

1. 在此节点下（根据您的特殊字符范围命名），添加以下两个属性：

   * **名称** `rangeStart`

      **类型** `Long`
      **值** the [Unicode](https://unicode.org/) 范围中第一个字符的表示（小数）

   * **名称** `rangeEnd`

      **类型** `Long`
      **值** the [Unicode](https://unicode.org/) 范围中最后一个字符的表示（小数）

1. 保存更改。

   例如，定义范围为9998 - 10000时，将提供以下字符。

   ![在CRXDE中，定义要在RTE中提供的字符范围](assets/chlimage_1-107.png)

   *图：在CRXDE中，定义要在RTE中提供的字符范围*

   ![RTE中提供的特殊字符会在弹出窗口中显示给作者](assets/rtepencil.png "RTE中提供的特殊字符会在弹出窗口中显示给作者")

## 配置表样式 {#tablestyles}

样式通常应用于文本，但样式集也可以应用于表格或几个表格单元格。 此类样式可供作者从单元格属性或表属性对话框的样式选择器框中创建。 在文本组件（或衍生组件）内编辑表时（而不是在标准的表组件中编辑表时），可以使用样式。

>[!NOTE]
您只能为经典UI定义表和单元格的样式。

>[!NOTE]
在RTE组件中或从RTE组件中复制和粘贴表依赖于浏览器。 并非所有浏览器都可开箱即用地支持此功能。 根据表结构和浏览器，可能会获得不同的结果。 例如，在经典UI和触屏UI的Mozilla Firefox中，复制并粘贴RTE组件中的表时，不会保留表的布局。

1. 在组件中，导航到节点 `<rtePlugins-node>/table`. 如果节点不存在，则创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 属性 `table` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*`

   >[!NOTE]
   如果不想启用所有表功能，可以创建 `features` 属性：
   * **类型** `String[]`
   * **值**(s)以下一项或两项，视需要而定：
      * `table` 允许编辑表属性；包括样式。
      * `cellprops` 以允许编辑单元格属性，包括样式。


1. 定义CSS样式表的位置以引用它们。 请参阅 [指定样式表的位置](#locationofstylesheet) 因为这与定义 [文本样式](#textstyles). 如果您定义了其他样式，则可以定义该位置。
1. 在 `table` 节点会根据需要创建以下节点：

   * 为整个表定义样式(位于 **[!UICONTROL 表属性]**):

      * **名称** `tableStyles`
      * **类型** `cq:WidgetCollection`
   * 定义单个单元格的样式(位于 **[!UICONTROL 单元格属性]**)、

      * **名称** `cellStyles`
      * **类型** `cq:WidgetCollection`


1. 创建节点(在 `tableStyles` 或 `cellStyles` 节点)来表示单个样式，

   * **名称** 您可以指定名称，但应反映样式。
   * **类型** `nt:unstructured`

1. 在此节点上，创建属性：

   * 要定义引用的CSS样式，

      * **名称** `cssName`
      * **类型** `String`
      * **值** CSS类的名称(不带前面的 `.`，例如， `cssClass` 而不是 `.cssClass`)
   * 要定义要在弹出选择器中显示的描述性文本，

      * **名称** `text`
      * **类型** `String`
      * **值** 要在选择列表中显示的文本


1. 保存所有更改。

对每个必需的样式重复上述步骤。

### 在表中配置隐藏的标题以辅助功能 {#hiddenheader}

有时，您可能会创建列标题中不带可视文本的数据表，这假定列与其他列的可视关系暗示了标题的用途。 在这种情况下，必须在标题单元格的单元格内提供隐藏的内部文本，以允许屏幕阅读器和其他辅助技术帮助具有各种需求的读者了解列的用途。

为了增强此类情况下的辅助功能，RTE支持隐藏的标头单元格。 此外，它还提供与表中隐藏标题相关的配置设置。 这些设置允许您在编辑和预览模式下对隐藏的标题应用CSS样式。 要帮助作者在编辑模式下识别隐藏的标题，请在代码中包含以下参数：

* `hiddenHeaderEditingCSS`:指定编辑RTE时，在隐藏标题单元格中应用的CSS类的名称。
* `hiddenHeaderEditingStyle`:指定编辑RTE时对隐藏标题单元格应用的样式字符串。

如果您在代码中同时指定CSS和样式字符串，则CSS类将优先于样式字符串，并可能会覆盖样式字符串所做的任何配置更改。

要帮助作者在预览模式下对隐藏的标题应用CSS，您可以在代码中包含以下参数：

* `hiddenHeaderClassName`:指定在预览模式下对隐藏的标题单元格应用的CSS类的名称。
* `hiddenHeaderStyle`:指定在预览模式下应用于隐藏标题单元格的样式字符串。

如果您在代码中同时指定CSS和样式字符串，则CSS类将优先于样式字符串，并可能会覆盖样式字符串所做的任何配置更改。

## 为拼写检查程序添加字典 {#adddict}

激活拼写检查插件后，RTE会对每种相应语言使用字典。 然后，根据网站的语言选择子树的语言属性或从URL中提取语言；例如。 the `/en/` 分支被检查为英语， `/de/` 分支为德语。

>[!NOTE]
消息“拼写检查失败”。 对于未安装的语言，如果尝试检查，则会显示。

标准Experience Manager安装包括以下字典：

* 美式英语(en_us)
* 英式英语(en_gb)

>[!NOTE]
标准字典位于 `/libs/cq/spellchecker/dictionaries`，以及相应的自述文件。 请勿修改文件。

要添加更多字典（如果需要），请执行以下步骤。

1. 导航到页面 [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. 选择所需的语言并下载包含拼写定义的ZIP文件。 提取文件系统上存档的内容。

   >[!CAUTION]
   只有 `MySpell` 支持OpenOffice.org v2.0.1或更早版本的格式。 由于字典现在是存档文件，因此建议您在下载后验证存档文件。

1. 找到.aff和.dic文件。 将文件名保留为小写。 例如， `de_de.aff` 和 `de_de.dic`.
1. 在存储库的以下位置加载.aff和.dic文件： `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
RTE拼写检查程序可按需使用。 在您开始键入文本时，它不会自动运行。
要运行拼写检查程序，请点按/单击工具栏中的拼写检查程序按钮。 RTE会检查单词拼写，并突出显示拼写错误的单词。
如果合并拼写检查器建议的任何更改，则文本更改的状态和拼写错误的词语将不再突出显示。 要运行拼写检查程序，请再次点按/单击拼写检查程序按钮。

## 为撤消和重做操作配置历史记录大小 {#undohistory}

RTE允许作者撤消或重做上次所做的一些编辑。 默认情况下，历史记录中会存储50个编辑内容。 您可以根据需要配置此值。

1. 在组件中，导航到节点 `<rtePlugins-node>/undo`. 如果这些节点不存在，请创建它们。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `undo` 节点创建属性：

   * **名称** `maxUndoSteps`
   * **类型** `Long`
   * **值** 希望保存在历史记录中的撤消步骤数。 默认为 50。使用 `0` 以完全禁用撤消/重做。

1. 保存更改。

## 配置选项卡大小 {#tabsize}

当在任何文本中按制表符时，会插入预定义的空格数；默认情况下，这是三个非中断空格和一个空格。

要定义制表符大小，请执行以下操作：

1. 在您的组件中，导航到节点 `<rtePlugins-node>/keys`. 如果节点不存在，则创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `keys` 节点创建属性：

   * **名称** `tabSize`
   * **类型** `String`
   * **值** 制表符使用的空格字符数。

1. 保存更改。

## 设置缩进边距 {#indentmargin}

启用缩进（默认）后，您可以定义缩进大小：

>[!NOTE]
此缩进大小仅应用于文本的段落（块）；它不会影响实际列表的缩进。

1. 在组件中，导航到节点 `<rtePlugins-node>/lists`. 如果这些节点不存在，请创建它们。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `lists` 节点创建 `identSize` 参数：

   * **名称**: `identSize`
   * **类型**: `Long`
   * **值**:缩进边距所需的像素数。

## 配置可编辑空间的高度 {#editablespace}

您可以定义组件对话框中显示的可编辑空间的高度。 仅当在对话框中使用RTE时，才适用配置。 配置不会更改对话框窗口的高度。

1. 在 `../items/text` 节点，在组件的对话框定义中，创建属性：

   * **名称** `height`
   * **类型** `Long`
   * **值** 编辑画布的高度（以像素为单位）。

1. 保存更改。

## 配置链接的样式和协议 {#linkstyles}

在 [!DNL Experience Manager]，您可以定义要使用的CSS样式和自动接受的协议。 配置链接在 [!DNL Experience Manager] 从其他程序中，定义HTML规则。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在与 `<rtePlugins-node>`，即在的父节点下创建节点 `<rtePlugins-node>`:

   * **名称** `htmlRules`
   * **类型** `nt:unstructured`

   >[!NOTE]
   的 `../items/text` 节点具有以下属性：
   * **名称** `xtype`
   * **类型** `String`
   * **值** `richtext`

   的位置 `../items/text` 节点可能会有所不同，具体取决于对话框的结构。 两个示例 `/apps/myProject>/components/text/dialog/items/text` 和 `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. 在 `htmlRules`，创建节点。

   * **名称** `links`
   * **类型** `nt:unstructured`

1. 在 `links` 节点根据需要定义属性：

   * 内部链接的CSS样式：

      * **名称** `cssInternal`
      * **类型** `String`
      * **值** CSS类的名称（不带前面的“。”）;例如， `cssClass` 而不是 `.cssClass`)
   * 外部链接的CSS样式

      * **名称** `cssExternal`
      * **类型** `String`
      * **值** CSS类的名称（不带前面的“。”）;例如， `cssClass` 而不是 `.cssClass`)
   * 有效数组 **[!UICONTROL 协议]** 包括 `https://`, `https://`, `file://`, `mailto:`，等

      * **名称** `protocols`
      * **类型** `String[]`
      * **值**&#x200B;一个或多个协议
   * **defaultProtocol** （类型的属性） **字符串**):用户未明确指定协议时使用的协议。

      * **名称** `defaultProtocol`
      * **类型** `String`
      * **值**&#x200B;一个或多个默认协议
   * 如何处理链接的目标属性的定义。 创建节点：

      * **名称** `targetConfig`
      * **类型** `nt:unstructured`

      在节点上 `targetConfig`:定义所需的属性：

      * 指定目标模式：

         * **名称** `mode`
         * **类型** `String`)
         * **值**(s):

            * `auto`:表示选择了自动目标

               (由 `targetExternal` 外部链接的属性或 `targetInternal` （内部链接）。

            * `manual`:不适用于此环境
            * `blank`:不适用于此环境
      * 内部链接的目标：

         * **名称** `targetInternal`
         * **类型** `String`
         * **值** 内部链接的目标(仅在模式为 `auto`)
      * 外部链接的目标：

         * **名称** `targetExternal`
         * **类型** `String`
         * **值** 外部链接的目标(仅在模式为 `auto`)。








1. 保存所有更改。
