---
title: 配置富文本编辑器，将内容作 [!DNL Adobe Experience Manager] 为Cloud Service。
description: 配置富文本编辑器，将内容 [!DNL Adobe Experience Manager] 作为Cloud Service。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 0%

---


# Configure the Rich Text Editor {#configure-the-rich-text-editor}

富文本编辑器(RTE)为作者提供了各种功能来编辑文本内容。 提供图标、选择框、工具栏和菜单，实现所见即所得的文本编辑体验。 管理员配置RTE以启用、禁用和扩展创作组件中的可用功能。 了解作者如 [何使用RTE创作](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) Web内容。

下面列出了RTE配置它所需的概念和步骤。

| 了解RTE概念 | 启用所需功能 | 配置单个功能 |
|---|---|---|
| [了解界面](#understand-rte-ui) | [了解和设置配置位置](#understand-the-configuration-paths-and-locations) | [配置插件](#enable-rte-functionalities-by-activating-plug-ins) |
| [编辑模式的类型](#editingmodes) | [激活插件](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [设置功能属性](#aboutplugins) |
| [关于插件](#aboutplugins) | [配置RTE工具栏](#dialogfullscreen) | [配置粘贴模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## 了解可供作者使用的用户界面 {#understand-rte-ui}

RTE界面优惠了响 [应式设计](/help/sites-cloud/authoring/features/responsive-layout.md) ，用于创作环境。 该界面设计用于触控和桌面设备。

![富文本编辑器工具栏](assets/rte-toolbar-full-screen-mode.png)

*图： 富文本编辑器工具栏，并启用所有可用选项。*

工具栏提供了“所见即所得”创作体验的选项。 [!DNL Experience Manager] 管理员可以配置界面工具栏中的可用选项。 默认情况下，在中提供一整套编辑选项 [!DNL Experience Manager]。 开发人员可以自 [!DNL Experience Manager] 定义以添加更多编辑选项。

## 各种编辑模式 {#editingmodes}

作者可以使用不同的组件 [!DNL Experience Manager] 模式创建和编辑文本内容。 用于创作内容和设置内容格式的工具栏选项以及不同编辑模式下启用RTE的组件的用户体验会因RTE配置而异。

| 编辑模式 | 编辑区域 | 建议启用的功能 |
|--- |--- |--- |
| 内嵌 | 就地编辑，实现快速、细微的编辑； 无需打开对话框即可设置格式。 | 最低RTE功能。 |
| RTE全屏 | 涵盖整个页面。 | 所有必需的RTE功能。 |
| 对话框 | 对话框，但不涵盖整个页面。 | 明智地启用功能。 |
| 全屏对话框 | 与全屏模式相同； 与RTE一起包含对话框的字段。 | 所有必需的RTE功能。 |

>[!NOTE]
>
>源代码编辑功能在内联编辑模式下不可用。 无法在全屏模式下拖动图像。 所有其他功能在所有模式下都有效。

### 内联编辑 {#inline-editing}

要编辑页面内的内容，请慢速单击多次以打开内容。 会显示一个包含基本选项的紧凑工具栏。

![使用工具栏中的基本选项进行内联编辑](assets/inline-editing-mode-basic-options.png)

*图： 使用工具栏中的基本选项进行内联编辑。*

### Full-screen editing {#full-screen-editing}

[!DNL Experience Manager] 组件可以以全屏视图打开，从而隐藏页面内容并占据可用屏幕。 考虑对内联编辑的详细版本进行全屏编辑，因为它优惠的编辑选项最多。 在使用内联编辑模 ![式时，可以通过单击图标](assets/rte_fullscreen.png)，从压缩工具栏全屏打开RTE。

在对话框全屏模式和详细的RTE工具栏中，对话框中的可用选项和组件也可用。 它仅适用于包含RTE和其他组件的对话框。

![以全屏模式进行编辑时的详细RTE工具栏](assets/rte-toolbar-full-screen-mode.png)

*图： 在全屏模式下进行编辑时显示的详细RTE工具栏。*

### 对话框编辑 {#dialog-editing}

当组件被多次单击时，将打开一个用于编辑内容的对话框。 现有页面顶部将打开对话框。 在某些特定情况下，对话框以弹出窗口的形式打开。 例如，当文本组件是多列页面布局中列的一部分，且对话框的可用区域较少时。

![对话框编辑模式](assets/dialog_editing_modetouchui.png)

*图： 对话框编辑模式。*

## 关于RTE插件和相关功能 {#aboutplugins}

该功能通过一系列插件提供，每个插件都具有：

* 一 `features` 个财产，

   * 用于激活或取消激活该插件的基本功能。
   * 使用标准化过程进行配置。

* 如果适用，需要进行专门配置的属性和选项会更多。

RTE的基本功能由特定于相应插件的节点上 `features` 的属性值激活或取消激活。

下表列表了当前插件，如下所示：

* 带有指向API文档的链接的插件ID。 激活插件时，ID将 [用作节点名称](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin)。
* 属性的允许 `features` 值。
* 插件提供的功能描述。

| 插件ID | 特征 | 描述 |
|--- |--- |--- |
| 编辑 | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [剪切、复制和，三种粘贴模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | 查找和替换。 |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [基本文本格式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [图像](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | 基本图像支持（从内容或内容查找器中拖动）。 根据浏览器的不同，支持对作者具有不同的行为 |
| [按键](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | 要定义此值，请参阅 [选项卡大小](configure-rich-text-editor-plug-ins.md#tabsize)。 |
| [证明](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`, `justifycenter`, `justifyright` | 段落对齐。 |
| [链接](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`, `unlink`, `anchor` | [超链接和锚点](configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| [列表](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | 此插件同时控制缩 [进和列表](configure-rich-text-editor-plug-ins.md#indentmargin); 包括嵌套列表。 |
| [错误工具](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`, `sourceedit` | 其他工具允许作者输入 [特殊字符](configure-rich-text-editor-plug-ins.md#spchar) 或编辑HTML源。 此外，如果要定 [义自己的列表](configure-rich-text-editor-plug-ins.md#definerangechar) ，还可以添加一系列特殊字符。 |
| 参数格式 | `paraformat` | 默认段落格式为段落、标题1、标题2和标`<p>`题3 `<h1>`(、 `<h2>`和 `<h3>`)。 您可以添 [加更多段落格式](configure-rich-text-editor-plug-ins.md#paraformats) 或扩展列表。 |
| 拼写检查 | `checktext` | [语言识别拼写检查器](configure-rich-text-editor-plug-ins.md#adddict)。 |
| 样式 | `styles` | 支持使用CSS类设置样式。 [如果要添加](configure-rich-text-editor-plug-ins.md#textstyles) （或扩展）您自己的样式范围以用于文本，请添加新的文本样式。 |
| 上标 | `subscript`, `superscript` | 基本格式的扩展，添加子脚本和超级脚本。 |
| 表 | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | 请参 [阅配置表样式](configure-rich-text-editor-plug-ins.md#tablestyles) ，为整个表或单个单元格添加您自己的样式。 |
| 撤消 | `undo`, `redo` | 撤消和重 [做操作的历史](configure-rich-text-editor-plug-ins.md#undohistory) 大小。 |

>[!NOTE]
>
>对话框模式不支持全屏插件。 使用设置 `dialogFullScreen` 将工具栏配置为全屏模式。

## 了解配置路径和位置 {#understand-the-configuration-paths-and-locations}

RTE [编辑模式和您为作者提供的界面](#editingmodes) ，决定了激活RTE插件时配置详细 [信息的位置](configure-rich-text-editor-plug-ins.md#activateplugin)。 位置包括：

* 内联模式： `cq:editConfig/cq:inplaceEditing`.
* 全屏模式: `cq:editConfig/cq:inplaceEditing`.
* 对话框模式： `cq:dialog`.
* 全屏对话框模式： `cq:dialog`.

>[!NOTE]
>
>请勿将节点命名为 `cq:inplaceEditing``config`。 在节 `cq:inplaceEditing` 点上，定义以下属性：
>
>* **名称**: `configPath`
>* **类型**: `String`
>* **值**: 包含实际配置的节点的路径

>
>
请勿将RTE配置节点命名为 `config`。 否则，RTE配置只对管理员有效，对组中的用户无效 `content-author`。

配置在对话框编辑模式下应用的以下属性：

* `useFixedInlineToolbar`: 您可以修复RTE工具栏而不是浮动工具栏。 将在RTE节点上定义的sling:resourceType=的布尔属性设 `cq/gui/components/authoring/dialog/richtext` 置为 `True`。 当此属性设置为 `True`时，将在事件上开始富文本编 `foundation-contentloaded` 辑。 要防止出现这种情况，请将属 `customStart` 性设 `True` 置为，并将 `rte-start` 事件触发为开始RTE编辑。 当此属性为 `true`时，RTE不开始单击，这是默认行为。

* `customStart`: 将在RTE节点上定义的此布尔属 `True`性设置为，通过触发开始控制何时事件RTE `rte-start`。

* `rte-start`: 在RTE事件编 `contenteditable-div` 辑RTE时触发此开始。 仅当设置为 `customStart` 时，它才可 `true`用。

在触屏启用对话框中使用RTE时，设置属性以 `useFixedInlineToolbar` 避 `true` 免出现问题。

## 通过激活插件启用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有features属性。 您可以配置features属性以启用或禁用每个插件的各种功能。

有关RTE插件的详细配置，请 [参阅如何激活和配置RTE插件](configure-rich-text-editor-plug-ins.md)。

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

核心 [组件文本组件允许模板编辑器](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) ，使用用户界面作为内容策略来配置许多RTE插件，从而无需进行技术配置。 内容策略可以如本文档所述使用RTE UI配置。 有关详细信息，请参 [阅创建页面模板](/help/sites-cloud/authoring/features/templates.md) 和核 [心组件开发人员文档](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)。

>为便于参考，默认文本组件（作为标准安装的一部分提供）可在以下位置找到：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
要创建您自己的文本组件，请复制上述组件，而不是编辑这些组件。

## 配置RTE工具栏 {#dialogfullscreen}

[!DNL Experience Manager] 允许您针对不同的编辑模式以不同方式配置富文本编辑器的界面。 默认设置如下所示。 您可以根据要求覆盖这些默认值。 您仅可自定义要提供给作者的工具栏功能。 您无需指定所有工具栏配置。

要配置工具栏，请 `dialogFullScreen`使用以下示例配置。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

内联模式和全屏模式使用不同的用户界面设置。 工具栏属性指定工具栏的选项。

例如，如果选项本身是功能(例如， `Bold`)，则它被指 `PluginName#FeatureName` 定为(例如 `links#modifylink`)。

如果该选项是弹出窗口（包含插件的某些功能），则指定 `#PluginName` 为(例如 `#format`)。

可以`|`使用指定一组选项之间的分隔符() `-`。

内嵌模式或全屏模式下的弹出节点包含正在使用的弹出画板的列表。 节点下的每个 `popovers` 子节点都以插件命名（例如，格式）。 它有一个属性“items”，其中包含插件功能的列表（例如，format#bold）。

## RTE用户界面设置和内容策略 {#rtecontentpolicies}

管理员可以使用内容策略控制RTE选项，例如，不要按照上述说明进行配置。 当内容策略用作可编辑模板的一部分时，内容策略会定义组件的 [设计属性](/help/sites-cloud/authoring/features/templates.md)。 例如，如果将使用RTE的文本组件与可编辑的模板一起使用，内容策略可以定义粗体选项可用，并提供一些段落格式选项。 内容策略可重复使用，并可以跨多个模板应用。

RTE流中从用户界面配置到内容策略的下游的可用选项。

* 用户界面配置设置定义了内容策略可用的选项。
* 如果删除或未启用RTE的用户界面配置，则内容策略无法配置它。
* 作者只能访问用户界面配置和内容策略提供的功能。

例如，您可以看到文本核 [心组件文档](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)。

## 自定义工具栏图标和命令之间的映射 {#iconstoolbar}

可以自定义RTE工具栏上显示的Coral图标与可用命令之间的映射。 除了Coral图标，您还不能使用任何其他图标。

1. 创建名为的 `icons` 节点 `uiSettings/cui`。

1. 为其下的各个图标创建节点。
1. 在每个单独的图标节点上，指定Coral图标和映射到该图标的命令。

下面是将命令映射到名为的 `Bold` Coral图标的示例代码 `textItalic`段。

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 已知限制 {#known-limitations}

[!DNL Experience Manager] RTE功能有以下限制：

* RTE功能仅在组件对话 [!DNL Experience Manager] 框中受支持。 向导或基础表单不支持RTE。

* [!DNL Experience Manager] 在混合设备上不工作。 <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* 请勿命名RTE配置节点 `config`。 否则，RTE配置仅对管理员有效，对组中的用户无效 `content-author`。

* RTE不支持在内联框架或iframe中嵌入内容。

## Best practices and tips {#best-practices-and-tips}

* 对于浮动对话框，请仅启用不带弹出对话框的插件。 没有弹出窗口的插件尺寸较小，最适合浮动对话框。
* 仅在全屏对话框模式或全屏模 `Paste` 式下，通过弹出窗口（如插件）启用插件。 具有大弹出窗口的插件需要更多屏幕空间来提供良好的创作体验。
* 如果您正在为CoralUI3 RTE使用自定义插件，请使用 `rte.coralui3` 库。

>[!MORELIKETHIS]
>
>* [配置RTE插件](configure-rich-text-editor-plug-ins.md)
>* [使用富文本编辑器进行创作](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [为可访问站点配置RTE](rte-accessible-content.md)
>* [创建复合多字段组件的教程范例](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

