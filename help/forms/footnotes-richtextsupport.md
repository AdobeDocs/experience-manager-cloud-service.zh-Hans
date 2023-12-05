---
title: 如何将脚注添加到自适应表单？
description: 对自适应表单中的脚注使用富文本编辑器(RTE) 。
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 12%

---

# 脚注组件 {#footnotecomponent}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

**[!UICONTROL 脚注]** 是显示在页面末尾的信息或注释的额外位。 [!UICONTROL 脚注] 由以数字作为上标的文本中指示的注释组成。

脚注会按照它们在页面上的显示顺序进行编号。 每个脚注都有一个唯一数字作为上标，该数字与放置在页面底部的数字相对应。 编号旁边将显示补充信息作为脚注说明。

![脚注描述](/help/forms/assets/footnote_description.png)


## 脚注的使用情况 {#usesoffootnotes}

* 帮助提供引用。
* 提供可中断主信息正常流动的额外信息。
* 提供括号信息或版权权限。

在自适应Forms中， [!UICONTROL 脚注] 用于显示有关如何完成或使用表单的信息。 有关如何创建自适应Forms的信息，请参阅 [创建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## 自适应Forms中的脚注 {#using-footnote-adaptiveforms}

要在自适应Forms中添加脚注，请执行以下步骤：
1. 在中打开自适应表单 **编辑** 模式。
1. 在组件浏览器中，拖放 **[!UICONTROL 文本]** 自适应表单上的组件。
1. 选择 **[!UICONTROL 文本]** 已添加并选择的组件 ![cmppr](assets/configure-icon.svg) 以编辑其属性。

   ![自适应Forms中的脚注](/help/forms/assets/footnote_rte.png)

1. 选择要为其添加脚注说明的文本，然后单击  ![星形](/help/forms/assets/asterisk.svg) 用于设置样式的按钮 **[!UICONTROL 脚注]** 组件。

1. 单击 ![check](/help/forms/assets/save_icon.svg) 以保存更改和样式。

   >[!NOTE]
   >
   >* 脚注会自动编号，并以在自适应表单中创建的方式显示。
   >* 如果存在重复的脚注，则所有重复的脚注的编号相同。

1. 在组件浏览器中，拖放 **[!UICONTROL 脚注占位符]** 自适应表单上的组件。
   >[!NOTE]
   >
   >* 在发布实例中，脚注显示在位置 **[!UICONTROL 脚注占位符]** 组件将放置在自适应表单上。
   >* 在不同面板之间导航时，只有可见的脚注会显示在 **[!UICONTROL 脚注占位符]** 导航面板中存在的属性。

1. 保存属性。

在运行时，数字以上标形式显示在文本上，其相应的说明显示在 **[!UICONTROL 脚注]** 位于以下位置的组件： [!UICONTROL 脚注占位符] 放置在自适应表单上。 您可以直接导航到脚注描述，方法是在 [!UICONTROL 脚注].


## 另请参阅 {#see-also}

{{see-also}}