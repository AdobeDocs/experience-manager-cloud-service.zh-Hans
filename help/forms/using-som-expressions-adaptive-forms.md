---
title: 如何在自适应Forms中使用SOM表达式？
description: 了解如何在自适应Forms中提取面板的SOM表达式。
feature: Adaptive Forms, Foundation Components
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 在自适应Forms中使用SOM表达式{#using-som-expressions-in-adaptive-forms}

自适应Forms建模为AEM页面，在AEM存储库中表示为JCR内容结构。 内容结构的关键元素是guideContainer节点。 guideContainer下方有rootPanel，其中可能包含嵌套面板和字段。

您可以使用脚本对象模型(SOM)来引用特定文档对象模型(DOM)中的值、属性和方法。 DOM以树层次结构组织内存对象和属性。 SOM表达式引用Fields/Draw元素和面板。

下图描述了将组件添加到表单时，自适应表单将翻译成的节点结构。 例如，您可以向根面板添加面板，并在面板中添加单选按钮，该按钮在运行时将转换为DOM。 自适应表单中单选按钮字段的SOM表达式指定为`guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`。

![DOM树](assets/hierarchy.png)

DOM树

自适应表单中任何元素的SOM表达式都以`guide[0].guide1[0]`为前缀。 组件在节点结构层次结构中的位置用于派生其SOM表达式。

带有两个单选按钮的![DOM树](assets/hierarchy_radio_button.png)

带两个单选按钮的DOM树

当您更改自适应表单中单选按钮的位置时，SOM表达式也会更改。 在创作模式下，您可以使用“查看SOM表达式”选项查看[!DNL AEM Forms]中字段或元素的SOM表达式。 右键单击字段或元素时，面板上会显示选项。

![在自适应表单中提取SOM表达式](assets/som-expressions.png)

在自适应表单中提取SOM表达式

在面板中，您可以从面板工具栏中访问该功能。 该功能有助于自适应表单作者编写脚本。

![使用面板工具栏提取SOM表达式](assets/som-expression.png)

使用面板工具栏提取SOM表达式

[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)中列出的某些API使用元素的SOM表达式。 例如，要将焦点置于自适应表单中的特定字段，请将相应的SOM表达式传递给`guideBridge`中的`getFocus`API。
