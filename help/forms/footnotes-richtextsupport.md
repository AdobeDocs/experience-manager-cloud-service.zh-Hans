---
title: 脚注支持
description: 对脚注的RTE支持。
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 脚注组件 {#footnotecomponent}

**[!UICONTROL 脚注]** 是显示在页面末尾的额外信息或注释位。 [!UICONTROL 脚注] 包含在文本中以数字作为上标的注释。

脚注按照它们在页面上的显示顺序进行编号。 每个脚注都有一个唯一的编号作为上标，该编号与置于页面底部的编号相对应。 数字旁边显示补充信息作为脚注描述。

![脚注描述](/help/forms/assets/footnote_description.png)


## 脚注的使用 {#usesoffootnotes}

* 帮助提供引证。
* 提供可中断主信息正常流的额外信息。
* 提供父信息或版权权限。

在自适应Forms中， [!UICONTROL 脚注] 用于显示有关如何填写或使用表单的信息。 有关如何创建自适应Forms的信息，请参阅 [创建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## 自适应Forms中的脚注 {#using-footnote-adaptiveforms}

要在自适应Forms中添加脚注，请执行以下步骤：
1. 在中打开自适应表单 **编辑** 模式。
1. 在组件浏览器中，拖放 **[!UICONTROL 文本]** 组件添加到自适应表单。
1. 选择 **[!UICONTROL 文本]** 添加和点按的组件 ![cppr](assets/configure-icon.svg) 以编辑其属性。

   ![自适应Forms中的脚注](/help/forms/assets/footnote_rte.png)

1. 选择要为其添加脚注说明的文本，然后单击  ![星星](/help/forms/assets/asterisk.svg) 样式 **[!UICONTROL 脚注]** 组件。

1. 单击 ![check](/help/forms/assets/save_icon.svg) 以保存更改和样式。

   >[!NOTE]
   >
   >* 脚注会自动编号，并以在自适应表单上创建的方式显示。
   >* 如果有重复的脚注，则所有重复的脚注的计数是相同的。


1. 在组件浏览器中，拖放 **[!UICONTROL 脚注占位符]** 组件添加到自适应表单。
   >[!NOTE]
   >
   >* 在发布实例中，脚注显示在 **[!UICONTROL 脚注占位符]** 组件会放置到自适应表单上。
   >* 在不同的面板之间导航时， **[!UICONTROL 脚注占位符]** 导航面板中存在的选件。


1. 保存属性。

运行时，数字会作为上标显示在文本中，并且其相应描述会显示在 **[!UICONTROL 脚注]** 组件的位置 [!UICONTROL 脚注占位符] 置于自适应表单上。 您可以通过单击 [!UICONTROL 脚注].