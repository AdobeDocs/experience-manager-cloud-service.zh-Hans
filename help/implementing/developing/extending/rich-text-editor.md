---
title: 将富文本编辑器配置为在 [!DNL Adobe Experience Manager] as a Cloud Service中创作内容。
description: 配置富文本编辑器以在 [!DNL Adobe Experience Manager] as a Cloud Service中创作内容。
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 7adfe0ca7fbab1f8a5bd488e524a48be62584966
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# 配置富文本编辑器 {#configure-the-rich-text-editor}

富文本编辑器(RTE)为作者提供了一系列广泛的功能来编辑文本内容。 为所见即所得文本编辑体验提供了图标、选择框、工具栏和菜单。 管理员配置RTE以启用、禁用和扩展创作组件中可用的功能。 查看作者[如何使用RTE创作](/help/sites-cloud/authoring/page-editor/rich-text-editor.md) Web内容。

下面列出了配置RTE所需的概念和步骤。

| 了解RTE概念 | 启用所需功能 | 配置单个功能 |
|---|---|---|
| [了解接口](#understand-rte-ui) | [了解并设置配置位置](#understand-the-configuration-paths-and-locations) | [配置插件](#enable-rte-functionalities-by-activating-plug-ins) |
| [编辑模式类型](#editingmodes) | [激活插件](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [设置功能属性](#aboutplugins) |
| [关于插件](#aboutplugins) | [配置RTE工具栏](#dialogfullscreen) | [配置粘贴模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## 了解可供作者使用的用户界面 {#understand-rte-ui}

RTE界面为创作环境提供了[响应式设计](/help/sites-cloud/authoring/page-editor/responsive-layout.md)。 该界面专为触控和桌面设备而设计。

![富文本编辑器工具栏](assets/rte-toolbar-full-screen-mode.png)

*图：已启用所有可用选项的RTF编辑器工具栏。*

工具栏提供了WYSIWYG创作体验的选项。 [!DNL Experience Manager]管理员可以在界面上的工具栏中配置可用选项。 默认情况下，[!DNL Experience Manager]中提供了一组完整的编辑选项。 开发人员可以自定义[!DNL Experience Manager]以添加更多编辑选项。

## 各种编辑模式 {#editingmodes}

作者可以使用不同的组件模式在[!DNL Experience Manager]中创建和编辑文本内容。 在不同编辑模式下，用于创作内容和设置内容格式的工具栏选项以及启用RTE的组件的用户体验因RTE配置而异。

| 编辑模式 | 编辑区域 | 建议启用的功能 |
|--- |--- |--- |
| 内嵌 | 就地编辑以进行快速次要编辑；格式化而不打开对话框。 | 最小的RTE功能。 |
| RTE全屏 | 涵盖整个页面。 | 所有必需的RTE功能。 |
| 对话框 | 对话框时，不会覆盖整个页面。 | 谨慎地启用功能。 |
| 全屏对话框 | 与全屏模式相同；包含对话框的字段以及RTE。 | 所有必需的RTE功能。 |

>[!NOTE]
>
>源编辑功能在内联编辑模式下不可用。 不能以全屏模式拖动图像。 所有其他功能在所有模式中都可用。

### 内联编辑 {#inline-editing}

要编辑页面中的内容，请通过缓慢双击打开内容。 呈现了一个包含基本选项的紧凑工具栏。

![使用工具栏中的基本选项进行内联编辑](assets/inline-editing-mode-basic-options.png)

*图：使用工具栏中的基本选项进行内联编辑。*

### 全屏编辑 {#full-screen-editing}

[!DNL Experience Manager]组件可以在隐藏页面内容并占用可用屏幕的全屏视图中打开。 请考虑全屏编辑内联编辑的详细版本，因为它提供了最多的编辑选项。 使用内联编辑模式时，可通过单击紧凑工具栏中的![图标以全屏方式打开RTE](assets/rte_fullscreen.png)，从而打开它。

在对话框的全屏模式下以及详细的RTE工具栏中，对话框中可用的选项和组件也可用。 它仅适用于包含RTE以及其他组件的对话框。

![在全屏模式下编辑时显示详细的RTE工具栏](assets/rte-toolbar-full-screen-mode.png)

*图：以全屏模式编辑时的详细RTE工具栏。*

### 对话框编辑 {#dialog-editing}

双击组件时，将打开一个对话框用于编辑内容。 对话框将在现有页面的顶部打开。 在某些特定情况下，对话框会作为弹出窗口打开。 例如，当文本组件属于多列页面布局中的列且可用于对话框的区域较少时。

![对话框编辑模式](assets/dialog_editing_modetouchui.png)

*图：对话框编辑模式。*

## 关于RTE插件和相关功能 {#aboutplugins}

该功能通过一系列插件提供，每个插件均具有：

* 一个`features`属性，

   * 用于激活或取消激活该插件的基本功能。
   * 使用标准化过程配置。

* 适当时，需要专门配置的更多属性和选项。

RTE的基本功能由相应插件专属的节点上的`features`属性值激活或停用。

下表列出了当前的插件，其中显示：

* 插件ID，以及API文档链接。 [激活插件](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin)时，将ID用作节点名称。
* `features`属性的允许值。
* 插件所提供的功能描述。

| 插件Id | 功能 | 描述 |
|--- |--- |--- |
| 编辑 | `cut`，`copy`，`paste-default`，`paste-plaintext`，`paste-wordhtml` | [剪切、复制和三种粘贴模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| findreplace | `find`、`replace` | 查找并替换。 |
| 格式 | `bold`、`italic`、`underline` | [基本文本格式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| 图像 | `image` | 基本图像支持（从内容或内容查找器拖动）。 根据浏览器的不同，支持的作者行为也有所不同 |
| 键 | - | 若要定义此值，请参阅[选项卡大小](configure-rich-text-editor-plug-ins.md#tabsize)。 |
| 两端对齐 | `justifyleft`、`justifycenter`、`justifyright` | 段落对齐方式。 |
| 链接 | `modifylink`、`unlink`、`anchor` | [超链接和锚点](configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| 列表 | `ordered`，`unordered`，`indent`，`outdent` | 此插件同时控制[缩进和列表](configure-rich-text-editor-plug-ins.md#indentmargin)；包括嵌套列表。 |
| misctools | `specialchars`、`sourceedit` | 其他工具允许作者输入[特殊字符](configure-rich-text-editor-plug-ins.md#spchar)或编辑HTML源。 此外，如果要定义自己的列表，可以添加[范围的特殊字符](configure-rich-text-editor-plug-ins.md#definerangechar)。 |
| 参数格式 | `paraformat` | 默认段落格式为段落、标题1、标题2和标题3 （`<p>`、`<h1>`、`<h2>`和`<h3>`）。 您可以[添加更多段落格式](configure-rich-text-editor-plug-ins.md#paraformats)或扩展列表。 |
| 拼写检查 | `checktext` | [语言感知拼写检查器](configure-rich-text-editor-plug-ins.md#adddict)。 |
| 样式 | `styles` | 支持使用CSS类进行样式设置。 如果要添加（或扩展）自己的样式范围以用于文本，请[添加新文本样式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| 下标 | `subscript`、`superscript` | 基本格式的扩展，添加了子脚本和超级脚本。 |
| 表 | `table`，`removetable`，`insertrow`，`removerow`，`insertcolumn`，`removecolumn`，`cellprops`，`mergecells`，`splitcell`，`selectrow`，`selectcolumns` | 请参阅[配置表样式](configure-rich-text-editor-plug-ins.md#tablestyles)，为整个表或单个单元格添加您自己的样式。 |
| 撤消 | `undo`、`redo` | [撤消和重做](configure-rich-text-editor-plug-ins.md#undohistory)操作的历史记录大小。 |

>[!NOTE]
>
>对话框模式不支持全屏插件。 使用`dialogFullScreen`设置将工具栏配置为全屏模式。

## 了解配置路径和位置 {#understand-the-configuration-paths-and-locations}

当您[激活RTE插件](configure-rich-text-editor-plug-ins.md#activateplugin)时，RTE编辑的[模式和您为作者提供的界面](#editingmodes)将决定配置详细信息的位置。 这些位置包括：

* 内联模式： `cq:editConfig/cq:inplaceEditing`。
* 全屏模式： `cq:editConfig/cq:inplaceEditing`。
* 对话框模式： `cq:dialog`。
* 全屏对话框模式： `cq:dialog`。

>[!NOTE]
>
>不要将`cq:inplaceEditing`下的节点命名为`config`。 在`cq:inplaceEditing`节点上，定义以下属性：
>
>* **名称**：`configPath`
>* **类型**：`String`
>* **值**：包含实际配置的节点的路径
>
>不要将RTE配置节点命名为`config`。 否则，RTE配置将仅对管理员生效，而不对组`content-author`中的用户生效。

配置以下在对话框编辑模式下应用的属性：

* `useFixedInlineToolbar`：您可以将RTE工具栏变为固定工具栏而不是浮动工具栏。 在sling：resourceType= `cq/gui/components/authoring/dialog/richtext`的RTE节点上将定义的此Boolean属性设置为`True`。 当此属性设置为`True`时，将在`foundation-contentloaded`事件上开始富文本编辑。 要防止出现这种情况，请将属性`customStart`设置为`True`并触发`rte-start`事件以开始RTE编辑。 当此属性为`true`时，单击时不会启动RTE，这是默认行为。

* `customStart`：将RTE节点上定义的此Boolean属性设置为`True`，以通过触发事件`rte-start`来控制何时启动RTE。

* `rte-start`：在开始编辑RTE时，在RTE的`contenteditable-div`上触发此事件。 仅当`customStart`设置为`true`时才有效。

在启用了触控的对话框中使用RTE时，将属性`useFixedInlineToolbar`设置为`true`以避免出现问题。

## 通过激活插件启用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有功能属性。 您可以配置features属性以启用或禁用每个插件的各种功能。

有关RTE插件的详细配置，请参阅[如何激活和配置RTE插件](configure-rich-text-editor-plug-ins.md)。

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

[核心组件文本组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)允许模板编辑器使用用户界面作为内容策略配置许多RTE插件，而无需技术配置。 内容策略可以与RTE UI配置配合使用，如本文档所述。 有关详细信息，请参阅[创建页面模板](/help/sites-cloud/authoring/page-editor/templates.md)和[核心组件开发人员文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)。

>出于参考目的，默认文本组件（作为标准安装的一部分提供）可以在以下位置找到：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>要创建您自己的文本组件，请复制上述组件而不是编辑这些组件。

## 配置RTE工具栏 {#dialogfullscreen}

[!DNL Experience Manager]允许您针对不同的编辑模式以不同的方式配置富文本编辑器的界面。 默认设置如下所示。 您可以根据自己的要求覆盖这些默认值。 您只需自定义要提供给作者的工具栏功能。 您无需指定所有工具栏配置。

要为`dialogFullScreen`配置工具栏，请使用以下示例配置。

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

例如，如果选项本身是功能（例如，`Bold`），则将其指定为`PluginName#FeatureName`（例如，`links#modifylink`）。

如果该选项是一个弹出窗口（包含插件的某些功能），则将其指定为`#PluginName`（例如，`#format`）。

可以使用`-`在选项组之间指定分隔符(`|`)。

内联或全屏模式下的弹出窗口节点包含正在使用的弹出窗口列表。 `popovers`节点下的每个子节点均以插件名称（例如，格式）命名。 它具有包含插件功能列表（例如，format#bold）的“items”属性。

## RTE用户界面设置和内容策略 {#rtecontentpolicies}

管理员可以使用内容策略来控制RTE选项，而不是执行如上所述的配置。 当内容策略用作[可编辑模板](/help/sites-cloud/authoring/page-editor/templates.md)的一部分时，它定义组件的设计属性。 例如，如果将使用RTE的文本组件与可编辑模板一起使用，则内容策略可以定义粗体选项是否可用，以及几个段落格式选项是否可用。 内容策略可重复使用，并且可以跨多个模板应用。

RTE中的可用选项会从用户界面配置下游流向内容策略。

* 用户界面配置设置定义哪些选项可用于内容策略。
* 如果RTE的用户界面配置已移除或未启用某个项目，则内容策略无法对其进行配置。
* 作者只能访问由用户界面配置和内容策略提供的功能。

例如，您可以看到[文本核心组件文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)。

## 自定义工具栏图标和命令之间的映射 {#iconstoolbar}

您可以自定义RTE工具栏上显示的Coral图标与可用命令之间的映射。 除了Coral图标之外，您无法使用任何其他图标。

1. 在`uiSettings/cui`下创建名为`icons`的节点。

1. 为下面的单个图标创建节点。
1. 在每个图标节点上，指定一个Coral图标和一个用于映射到该图标的命令。

以下是将命令`Bold`映射到名为`textItalic`的Coral图标的示例片段。

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

[!DNL Experience Manager] RTE功能具有以下限制：

* 仅在[!DNL Experience Manager]组件对话框中支持RTE功能。 向导或Foundation-forms不支持RTE。

* [!DNL Experience Manager]在混合设备上不起作用。<!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* 不要命名RTE配置节点`config`。 否则，RTE配置仅对管理员生效，而不对组`content-author`中的用户生效。

* RTE不支持将内容嵌入到内联框架或iframe中。

## 最佳实践和提示 {#best-practices-and-tips}

* 对于浮动对话框，请仅启用插件而不启用弹出对话框。 没有弹出窗口的插件尺寸较小，最适合用于浮动对话框。
* 仅在全屏对话框模式或全屏模式下通过较大的弹出窗口启用插件，如`Paste`插件。 具有大型弹出窗口的插件需要更多的屏幕空间才能提供良好的创作体验。
* 如果要使用CoralUI3 RTE的自定义插件，请使用`rte.coralui3`库。

>[!MORELIKETHIS]
>
>* [配置RTE插件](configure-rich-text-editor-plug-ins.md)
>* [使用富文本编辑器进行创作](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)
>* [为可访问的站点配置RTE](rte-accessible-content.md)
