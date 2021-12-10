---
title: 自适应Forms中的分隔符组件
seo-title: Separator component in Adaptive Forms
description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# 自适应Forms中的分隔符组件{#separator-component-in-adaptive-forms}

可以使用分隔符组件以可视方式分隔表单的面板。 您可以通过指定分隔符组件的以下属性来定义分隔符组件的整体外观和样式：

* **元素名称：** 指定组件的名称。 SOM表达式使用元素名称字段中指定的值来寻址组件。
* **厚度：** 以像素为单位指定分隔符组件的厚度。

* **CSS类：** 指定分隔符组件的自定义CSS类

* **内联样式：** 使用 [!DNL AEM Forms]，您现在可以将内联CSS样式应用于单个自适应表单组件并实时预览更改。

您可以使用布局模式定义分隔符组件跨越的列数。 有关更多信息，请参阅 [使用布局模式调整组件大小](resize-using-layout-mode.md).

要指定分隔符组件的属性，请执行以下操作：

1. 选择分隔符组件并点按 ![cppr](assets/cmppr.png). 将在侧栏中打开属性。
1. 单击内联CSS属性部分中的选项卡以指定CSS属性。 例如：a.在字段选项卡中，单击 **添加项目**. 将添加一行包含两个字段。
1. 在左侧的第一个字段中，指定要应用的CSS3属性。 例如， **边框**. 您还可以通过单击向下箭头按钮来选择属性。 下拉列表并不详尽，您可以在此字段中指定任何受支持的CSS3属性名称。
1. 在相邻的字段中，为指定的CSS3属性指定有效值。 例如， **3像素纯黑色**.
1. 单击 **添加项目** 以指定其他属性及其值。
1. 单击 **预览** 以预览表单中的更改。
1. 单击 **确定** 确认更改或 **取消** ，以退出对话框而不进行任何更改。

