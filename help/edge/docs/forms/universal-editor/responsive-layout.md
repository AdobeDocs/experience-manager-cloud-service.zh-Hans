---
title: 了解通用编辑器 — 响应模式
description: 本文介绍了如何使用通用编辑器中的不同模拟器预览表单，以在创作过程中可视化表单的外观。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 1%

---


# WYSIWYG创作中的响应模式

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将包含您的GitHub组织名称和存储库名称的电子邮件(从您的官方地址发送到<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> )。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>

## 响应式Forms简介

在当今的多设备世界中，从台式机显示器到智能手机，各种大小的屏幕都需要您的表单外观美观且功能良好。 通用编辑器中的响应模式允许您在创作过程中预览和测试跨不同设备大小的表单，从而帮助您实现此目标。

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)使您能够创建自动适应不同屏幕大小的表单，从而提供最佳用户体验，而不管使用的是什么设备。

## 在不同设备的响应模式下预览Forms

通用编辑器在屏幕的右上角提供了&#x200B;**模拟器**&#x200B;图标，允许您预览不同设备大小的页面，并测试响应式设计的行为，以获得更好的用户体验。

要在响应模式下预览表单，请执行以下操作：

1. 在通用编辑器中打开窗体以进行编辑。
2. 单击工具栏中显示设备预览符号![&#128279;](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%，width=2%}图标的模拟器图标。
3. 选择设备格式：
   - 桌面（默认）
   - 平板电脑
   - 移动设备
   - 自定义（指定宽度和高度）

![通用编辑器屏幕截图显示不同设备的响应模式选项](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

在平板电脑或移动设备上预览时，您还可以使用&#x200B;**屏幕旋转器**&#x200B;图标在纵向和横向之间切换。

通用编辑器提供了不同的模拟器来预览各种设备上的表单。 下表列出了可用的模拟器类型及其相应的设备表示形式：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模拟器类型</th>
        <th style="width: 80%">设备图像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌面</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="显示全宽布局的表单的桌面视图" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板电脑</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="显示具有已调整组件的中等宽度布局的表单的平板电脑视图" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">移动设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="显示具有栈叠组件的窄布局的表单的移动视图" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自定义设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="具有用户指定维度的表单的自定义设备视图" style="width: auto; height: auto"></td>
    </tr>
</table>

## 布局功能

通用编辑器允许您创建易于使用的表单，为最终用户提供动态体验。 表单布局控制项或组件在表单中的显示方式。

通用编辑器支持以下类型的表单布局：

- [面板布局](#panel-layout)
- [向导布局](#wizard-layout)
- [可折叠项布局](#accordion-layout)

### 面板布局

面板布局有助于以更便于导航和查找相应内容的方式组织相关字段。 面板布局将表单组件排列在表单的不同部分或面板中。

![在一个表单中显示多个不同部分的面板布局](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**示例：**&#x200B;工作申请表单可能使用面板将“个人信息”、“教育”、“工作体验”和“引用”分隔为不同的部分。

**响应式行为：**&#x200B;在较小的屏幕上，面板通常垂直栈叠，在调整到较窄的宽度时保持其不同的分组。

您可以使用[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表单中添加面板布局。 有关如何配置面板组件的各种属性的详细说明，请参阅[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)文章。

### 向导布局

向导布局可将复杂表单划分为不同的步骤，从而帮助简化该表单。 每个步骤代表流程的不同部分，用户按顺序浏览这些步骤，通常使用&#x200B;**下一步**&#x200B;和&#x200B;**上一步**&#x200B;按钮。 您可以使用向导布局创建包含多个部分或步骤的表单。

![向导布局显示具有导航控制项的多步骤表单](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**示例：**&#x200B;保险索赔表单可能使用向导引导用户提供事件详细信息、上传证据、输入个人信息和查看提交。

**响应行为：**&#x200B;在移动设备上，向导会保持其分步方式，但会调整每个步骤中的内容以适合较窄的屏幕，通常是将并排显示在较大屏幕上的元素栈叠在一起。

您可以使用[向导组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表单中添加向导布局。 有关如何配置向导组件的各种属性的详细说明，请参阅[向导组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)一文。

### 可折叠项布局

折叠布局在自适应表单中以可折叠部分或面板显示内容。 展开某个部分时，会在其中显示内容，而其他部分仍保持折叠状态。 此布局非常适用于以紧凑形式显示大量信息。

![显示表单中可展开部分的折叠布局](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**示例：**&#x200B;产品配置表单可能使用“基本选项”、“高级功能”、“附件”和“付款计划”的可折叠项部分，使用户一次只能关注一个方面。

**响应式行为：**&#x200B;折叠面板在移动设备上效果特别好，因为它们仅显示扩展的内容部分，自然会节省垂直空间，非常适合较小的屏幕。

您可以使用[折叠组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表单中添加折叠布局。 有关如何配置折叠组件的各种属性的详细说明，请参阅[折叠组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)文章。

### 如何选择正确的布局？

选择正确的布局以优化用户体验和表单功能很重要。 该表可帮助您了解可用的各种布局选项，并指导您根据特定需求和用例选择最合适的布局：

| 专题 | 面板布局 | 向导布局 | 可折叠项布局 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **目的** | 将相关内容分组为不同的部分 | 指导用户完成多步骤流程或表单 | 将内容整理到可折叠部分中 |
| **结构** | 不同的部分 | 连续步骤/页面 | 可折叠面板/区域 |
| **导航** | 单击面板标题以进行导航 |  — 前进：“下一步”按钮<br> — 后退：“后退”按钮<br> — 可选跳过步骤 | 单击标题可展开/折叠部分 |
| **用户体验** | 以可管理的方式组织大量内容 | 逐步指导，减少负担 | 具有展开/折叠部分的紧凑视图 |
| **用例** | 具有已分类分区的复杂表单 | 设置流程，复杂表单 | 常见问题解答、设置菜单、详细内容部分 |
| **最适合移动设备** | 审核 — 面板垂直栈叠 | 良好 — 仅关注当前步骤 | 优秀 — 使用可折叠部分节省空间 |

## 针对响应式Forms的最佳实践

要确保您的表单在所有设备上提供最佳体验，请遵循以下最佳实践：

1. **首先针对移动设备进行设计：**&#x200B;首先针对移动设备设计表单，然后针对更大的屏幕进行增强。 此方法可确保核心功能在最小的屏幕上正常工作。

2. **使用适当的字段类型：**&#x200B;选择在触控设备上运行良好的字段类型：
   - 当有许多选项时，请使用下拉菜单而不是单选按钮
   - 使用为触摸输入而设计的日期选取器
   - 确保按钮和触摸目标至少为44px x 44px

3. **简化小屏幕：**
   - 在移动设备上每行显示的字段较少
   - 考虑在“显示更多”选项后面隐藏可选字段
   - 在移动设备上将复杂表单划分为更多步骤

4. **彻底测试：**&#x200B;始终在实际设备上测试表单，或使用通用编辑器中的模拟器模式测试表单，以确保它们在屏幕大小之间正常运行。

5. **考虑加载时间：**&#x200B;优化图像大小并最小化所需资源，尤其是对于连接速度较慢的移动用户。

## 响应式Forms故障诊断

| 问题 | 可能的原因 | 解决方案 |
|-------|---------------|----------|
| 在移动设备上表单显示为被切断 | 修复了宽度设置或溢出问题 | 使用相对单位(%， rem)而不是像素，并检查溢出：隐藏属性 |
| 难以与交互的触摸元素 | 接触目标太小或太接近 | 将按钮/输入大小至少增加到44像素x 44像素，并在交互式元素之间增加更多空间 |
| 小屏幕上的内容溢出 | 对于较小的视区，无响应规则 | 添加媒体查询或响应类以调整不同屏幕大小的布局 |
| 在移动设备上表单速度太慢 | 大图像或过多的脚本 | 优化图像，最小化JavaScript，并考虑延迟加载非关键元素 |
| 模拟器和实际设备之间的外观不同 | 浏览器特定的呈现或设备变量 | 尽可能在实际设备上测试，而不仅仅是模拟器 |

## 另请参阅

{#see-more-eds-forms}
