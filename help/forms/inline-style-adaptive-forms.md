---
title: 如何将内联样式应用到自适应表单组件？
description: 虽然您可以在自适应表单上应用自定义样式，但也可以在自适应表单的各个组件上应用内联CSS属性。 了解如何将内联样式应用到自适应表单组件。 使用示例深入挖掘，将内嵌样式应用于文本字段组件。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# 自适应表单组件的内联样式 {#inline-styling-of-adaptive-form-components}

您可以通过使用指定样式来定义自适应表单的整体外观和样式 [主题编辑器](themes.md). 此外，您还可以将内联CSS样式应用于单个自适应表单组件，并即时预览更改。 内联样式会覆盖主题中提供的样式。

## 应用内联CSS属性 {#apply-inline-css-properties}

要向组件添加内联样式，请执行以下操作：

1. 在表单编辑器中打开表单，然后将模式更改为样式模式。 要将模式更改为样式模式，请在页面工具栏中，点按 ![画布下拉列表](assets/Smock_ChevronDown.svg) > **[!UICONTROL 样式]**.
1. 在页面中选择组件，然后点按编辑按钮 ![edit-button](assets/edit.svg). 在侧栏中打开样式属性。

   您还可以从侧栏的表单层次结构树中选择组件。 表单层次结构树在侧栏中可用作表单对象。

   在 [!UICONTROL 样式] 模式下，您可以看到“表单对象”下列出的组件。 但是，侧栏中的“表单对象”列表会列出字段和面板等组件。 字段和面板是可包含文本框和单选按钮等组件的通用组件。

   从侧栏中选择组件时，您会看到列出的所有子组件以及选定组件的属性。 您可以选择特定子组件并设置其样式。

1. 单击侧栏中的选项卡以指定CSS属性。 您可以指定以下属性：

   * [!UICONTROL Dimension和位置] （显示设置、内边距、高度、宽度、边距、位置、z指数、浮动、清除、溢出）
   * [!UICONTROL 文本] （字体系列、粗细、颜色、大小、行高和对齐方式）
   * [!UICONTROL 背景] （图像和渐变、背景颜色）
   * [!UICONTROL 边框] （宽度、样式、颜色、半径）
   * [!UICONTROL 效果] （阴影、不透明度）
   * [!UICONTROL 高级] （允许您为组件编写自定义CSS）

1. 同样，您也可以为组件的其他部分应用样式，例如 [!UICONTROL 构件], [!UICONTROL 题注]和 [!UICONTROL 帮助].
1. 点按 **[!UICONTROL 完成]** 确认更改或 **[!UICONTROL 取消]** 以放弃更改。

## 示例：字段组件的内联样式 {#example-inline-styles-for-a-field-component}

以下图像描述了将内联样式应用于文本字段前后的文本字段。

![应用内联样式之前的文本框组件](assets/no-style.png)

应用内联样式属性之前的文本框组件

请注意，在应用以下CSS属性后，文本框样式发生了更改，如下图所示。

<table>
 <tbody>
  <tr>
   <td><p>选择器</p> </td>
   <td><p>CSS属性</p> </td>
   <td><p>值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>字段</p> </td>
   <td><p>边框</p> </td>
   <td><p>边框宽度= 2像素</p> <p>边框样式=实线</p> <p>边框颜色=#1111</p> </td>
   <td><p>在字段周围创建一个黑色的2像素宽边框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>将背景颜色更改为玉米花蓝色(#6495ED)</p> <p>注意：您可以在值字段中指定颜色名称或其十六进制代码。</p> </td>
  </tr>
  <tr>
   <td><p>标签</p> </td>
   <td><p>Dimension和位置&gt;宽度</p> </td>
   <td><p>100px</p> </td>
   <td><p>将标签的宽度修复为100像素</p> </td>
  </tr>
  <tr>
   <td>字段帮助图标</td>
   <td>文本&gt;字体颜色</td>
   <td>#2ECC40</td>
   <td>更改帮助图标面的颜色。</td>
  </tr>
  <tr>
   <td><p>长描述</p> </td>
   <td><p>text-align</p> </td>
   <td><p>居中</p> </td>
   <td><p>将帮助的长说明与中心对齐</p> </td>
  </tr>
 </tbody>
</table>

![应用内联样式后的文本框样式](assets/applied-style.png)

应用内联样式属性后的文本框组件

按照上述步骤，您可以选择其他组件（如面板、提交按钮和单选按钮）并设置其样式。

>[!NOTE]
>
>样式属性因您选择的组件而异。

## 复制并粘贴样式 {#copy-paste-styles}

您还可以在自适应表单中将样式从一个组件复制并粘贴到另一个组件。 在 **[!UICONTROL 样式]** 模式时，点按组件，然后点按复制图标 ![复制](assets/property-copy-icon.svg).

点按同一类型的其他组件，然后点按粘贴图标 ![复制](assets/Smock_Paste_18_N.svg) 以粘贴复制的样式。 您还可以点按清除样式图标 ![复制](assets/clear-style-icon.svg) 以清除应用的样式。

## 为组件的不同状态设置样式 {#set-styles-for-states}

您可以为组件类型的不同状态设置样式。 不同状态包括： [!UICONTROL 焦点], [!UICONTROL 已禁用], [!UICONTROL 悬停], [!UICONTROL 错误], [!UICONTROL 成功]和 [!UICONTROL 必需].

要为组件状态定义样式，请执行以下操作：

1. 在 **[!UICONTROL 样式]** 模式时，点按组件，然后点按编辑图标 ![编辑](assets/Smock_Edit_18_N.svg).

1. 使用 **[!UICONTROL 州]** 下拉列表。

   ![选择状态](assets/select-state.png)

1. 为组件的选定状态定义样式，然后点按 ![保存](assets/save_icon.svg) 以保存属性。

您还可以模拟成功和错误状态。 点按展开图标以查看 **[!UICONTROL 模拟成功]** 和 **[!UICONTROL 模拟错误]** 选项。

![模拟状态](assets/simulate-states.png)
