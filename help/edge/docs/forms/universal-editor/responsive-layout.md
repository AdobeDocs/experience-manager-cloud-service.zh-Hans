---
title: 了解通用编辑器——响应式模式
description: 本文介绍了如何在通用编辑器中使用不同的模拟器预览表单，以便在创作过程中直观地了解其外观。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: ht
source-wordcount: '1247'
ht-degree: 100%

---


# 所见即所得创作中的响应式模式

<span class="preview">这是一项通过<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features">预发布渠道</a>提供的预发布功能。</span>

## 响应式表单简介

在当今的多设备世界中，您的表单需要在各种尺寸的屏幕上（从台式机显示器到智能手机）看起来美观且运行良好。通用编辑器中的响应式模式通过让您在创作过程中预览和测试表单在不同设备尺寸下的表现，从而帮助您实现这一目标。

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)使您能够创建自动适应不同屏幕尺寸的表单，无论使用何种设备都能提供最佳的用户体验。

## 在不同设备上以响应式模式预览表单

通用编辑器在屏幕的右上角提供了一个&#x200B;**模拟器**&#x200B;图标，该图标允许您预览不同设备尺寸的页面，并测试您的响应式设计行为，以获得更好的用户体验。

要在响应式模式下预览表单：

1. 在通用编辑器中打开表单以进行编辑。
2. 单击工具栏中的![显示设备预览符号的模拟器](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%}图标。
3. 选择设备格式：
   - 桌面（默认）
   - 平板电脑
   - 移动设备
   - 自定义（指定宽度和高度）

![通用编辑器的屏幕快照，显示了不同设备的响应式模式选项](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

您还可以使用&#x200B;**屏幕旋转器**&#x200B;图标在平板电脑或移动设备上进行预览时，在纵向和横向之间进行切换。

通用编辑器提供不同的模拟器，以便在各种设备上预览表单。下表列出了可用的模拟器类型，及其相应的设备表示：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模拟器类型</th>
        <th style="width: 80%">设备图像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌面</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="表单的桌面视图，展示全宽布局" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板电脑</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="表单的平板电脑视图，显示中等宽度的布局，并调整了组件" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">移动设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="表单的移动设备视图，展示窄版布局，并且组件堆叠排列" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自定义设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="具有用户指定尺寸的表单的自定义设备视图" style="width: auto; height: auto"></td>
    </tr>
</table>

## 布局能力

通用编辑器允许您创建易于使用的表单，可为最终用户提供动态体验。表单布局控制表单中项目或组件的显示方式。

通用编辑器支持以下类型的表单布局：

- [面板布局](#panel-layout)
- [向导布局](#wizard-layout)
- [折叠布局](#accordion-layout)

### 面板布局

面板布局对于组织相关字段很有帮助，它使得导航和查找相应内容变得更加容易。面板布局将表单组件排列在表单中的不同部分或面板内。

![面板布局显示表单内的多个不同部分](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**示例：**&#x200B;工作申请表可能会使用面板将“个人信息”、“教育”、“工作经验”和“推荐人”分成不同的部分。

**响应式行为：**&#x200B;在较小的屏幕上，面板通常垂直堆叠，保持其独特的分组，同时调整到较窄的宽度。

您可以使用[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表单中添加面板布局。有关如何配置面板组件各种属性的详细说明，请参阅[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)一文。

### 向导布局

向导布局通过将复杂的表单分解为不同的步骤来帮助简化表单。每个步骤代表该流程的不同部分，用户按顺序浏览各个步骤，期间通常会使用&#x200B;**前进**&#x200B;和&#x200B;**后退**&#x200B;按钮。您可以使用向导布局来创建涉及多个部分或步骤的表单。

![向导布局显示带有导航控件的多步骤表单](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**示例：**&#x200B;保险索赔表可能会使用向导来指导用户提供事故详细信息、上传证据、输入个人信息以及审查提交内容。

**响应式行为：**&#x200B;在移动设备上，向导保持逐步推进的方式，但会调整每个步骤中的内容，以适应较窄的屏幕，并且通常会将原本在大屏幕上并排显示的元素堆叠起来。

您可以使用[向导组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表单中添加向导布局。有关如何配置向导组件各种属性的详细说明，请参阅[向导组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)一文。

### 折叠布局

折叠布局在自适应表单中以可折叠的部分或面板显示内容。当某个部分展开时，它会显示其中的内容，而其他部分则保持折叠状态。这种布局非常适合以紧凑的形式显示大量信息。

![显示表单中可展开部分的折叠布局](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**示例：**&#x200B;产品配置表单可能会使用折叠部分来表示“基本选项”、“高级功能”、“配件”和“付款计划”，以便用户一次关注一个方面。

**响应式行为：**&#x200B;折叠布局在移动设备上特别有效，因为它们通过仅显示展开的内容部分自然地节省了垂直空间，使其非常适合较小的屏幕。

您可以使用[折叠组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表单中添加折叠布局。有关如何配置折叠组件各种属性的详细说明，请参阅[折叠组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)一文。

### 如何选择合适的布局？

选择合适的布局来优化用户体验和表单功能非常重要。该表可帮助您了解不同的布局选项，并指导您根据特定需求和用例选择最合适的布局：

| 功能 | 面板布局 | 向导布局 | 折叠布局 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **用途** | 将相关内容分组为不同的部分 | 引导用户完成多步骤流程或填写表格 | 将内容组织成可折叠的部分 |
| **结构** | 不同的部分 | 连续步骤/页面 | 可折叠面板/部分 |
| **导航** | 单击面板标头来进行导航 | - 前进：“下一步”按钮<br>- 后退：“返回”按钮<br>- 跳过步骤（可选） | 单击标头可展开/折叠相关部分 |
| **用户体验** | 以可管理的方式组织大量内容 | 逐步指导，减少压力 | 带有展开/折叠部分的紧凑视图 |
| **用例** | 具有分类部分的复杂表单 | 设置流程，复杂表单 | 常见问题解答、设置菜单、详细内容部分 |
| **最适合移动设备** | 中等——面板垂直堆叠 | 好——仅关注当前步骤 | 非常好——通过可折叠部分节省空间 |

## 响应式表单的最佳实践

为了确保您的表单在所有设备上提供最佳体验，请遵循以下最佳实践：

1. **首先为移动设备进行设计：**&#x200B;首先设计适用于移动设备的表单，然后针对更大的屏幕进行增强。这种方法可确保核心功能即使在最小的屏幕上也能运行。

2. **使用适当的字段类型：**&#x200B;选择适合触摸设备的字段类型：
   - 当有多个选项时，使用下拉菜单而不是单选按钮
   - 使用专为触摸输入设计的日期选择器
   - 确保按钮和触摸目标至少为 44px x 44px

3. **为较小屏幕简化设计：**
   - 在移动设备上每行显示更少的字段
   - 考虑将可选字段隐藏在“显示更多”选项后面
   - 在移动设备上将复杂的表单分解为更多步骤

4. **彻底测试：**&#x200B;务必在实际设备上或使用通用编辑器中的模拟器模式测试您的表单，以确保它们在不同屏幕尺寸下都能正常运行。

5. **考虑加载时间：**&#x200B;优化图像大小并尽量减少所需资源，特别是对于连接速度较慢的移动用户。

## 响应式表单故障排除

| 问题 | 可能的原因 | 解决方案 |
|-------|---------------|----------|
| 表单在移动设备上显示被截断 | 固定宽度设置或溢出问题 | 请使用相对单位（如 %、rem）代替像素单位，并检查 overflow:hidden 属性 |
| 触摸元素难以交互 | 触摸目标太小或距离太近 | 将按钮/输入尺寸增加到至少 44px x 44px，并在交互元素之间添加更多空间 |
| 内容在小屏幕上溢出 | 对于较小的视口没有响应规则 | 添加媒体查询或响应类别来调整不同屏幕尺寸的布局 |
| 移动设备上的表单速度太慢 | 大图像或脚本过多 | 优化图像，最小化 JavaScript，并考虑对非关键元素进行延迟加载 |
| 模拟器和真实设备之间的外观差异 | 特定于浏览器的渲染或设备变化 | 尽可能在实际设备上进行测试，而不仅仅是模拟器 |

## 另请参阅

{#see-more-eds-forms}
