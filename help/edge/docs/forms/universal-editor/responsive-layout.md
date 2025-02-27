---
title: 了解通用编辑器 — 响应模式
description: 本文介绍了如何使用通用编辑器中的不同模拟器预览表单，以在创作过程中可视化表单的外观。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# WYSIWYG创作中的响应模式

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将您的正式地址中的电子邮件发送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub组织名称和存储库名称。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>


[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)允许您使用不同的模拟器预览Edge Delivery Services Forms，以便在创作过程中查看表单的外观。

响应模式允许开发人员设计自动适应不同屏幕大小的布局，包括台式机、平板电脑和移动设备。 通用编辑器支持适用于台式机、平板电脑和移动设备的模拟器。 您可以根据屏幕大小设置高度和宽度，然后执行以下操作：

* 设置方向
* 指定宽度和高度
* 更改方向

## 在不同设备的响应模式下预览Forms

通用编辑器在屏幕的右上角提供了&#x200B;**模拟器**&#x200B;图标，允许您预览不同设备大小的页面，并测试响应式设计的行为，以获得更好的用户体验。

要了解通用编辑器如何在不同屏幕大小上呈现表单，请执行以下步骤：

1. 在通用编辑器中打开窗体以进行编辑。
1. 选择通用编辑器工具栏上可用的![模拟器图标](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%，width=2%}，然后单击模拟器图标以显示该选项。

   ![响应模式](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. 选择一个选项以在选定的设备上在通用编辑器中模拟表单：桌面、平板电脑、移动设备。

   ![响应模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%，height=40%}

   默认情况下，编辑器会在桌面布局中打开，其高度和宽度由浏览器自动确定。 或者，您可以在移动或平板电脑设备上模拟表单。 您还可以自定义自定义设备的屏幕宽度和高度。

通用编辑器提供了不同的模拟器来预览各种设备上的表单。 下表列出了可用的模拟器类型及其相应的设备表示形式：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模拟器类型</th>
        <th style="width: 80%">设备图像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌面</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="桌面模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板电脑</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="平板电脑模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">移动设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="移动设备模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自定义设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="自定义设备模拟器" style="width: auto; height: auto"></td>
    </tr>
</table>

在不同设备上预览表单时，可以使用&#x200B;**屏幕旋转器**&#x200B;图标在纵向和横向之间切换。 它可帮助开发人员测试响应式设计如何适应各种设备上的屏幕旋转。

通用编辑器支持各种表单布局。 要浏览不同的布局，请参阅[布局功能](#layout-capabilities)部分。

## 布局功能

通用编辑器允许您创建易于使用的表单，为最终用户提供动态体验。 表单布局控制项或组件在表单中的显示方式。

通用编辑器支持以下类型的表单布局：
* [面板布局](#panel-layout)
* [向导布局](#wizard-layout)
* [可折叠项布局](#accordion-layout)

### 面板布局

面板布局有助于以更便于导航和查找相应内容的方式组织相关字段。 面板布局将表单组件排列在表单的不同部分或面板中。

![面板布局](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

您可以使用[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表单中添加面板布局。 有关如何配置面板组件的各种属性的详细说明，请参阅[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)文章。

### 向导布局


向导布局通过将复杂表单划分为不同的步骤来帮助简化该表单。 每个步骤代表流程的不同部分，用户按顺序浏览这些步骤，通常使用&#x200B;**下一步**&#x200B;和&#x200B;**上一步**&#x200B;按钮。 您可以使用向导布局创建包含多个部分或步骤的表单。

![向导布局](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

您可以使用[向导组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表单中添加向导布局。 有关如何配置向导组件的各种属性的详细说明，请参阅[向导组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)一文。

### 可折叠项布局

折叠布局在自适应表单中以可折叠部分或面板显示内容。 展开某个部分时，会在其中显示内容，而其他部分仍保持折叠状态。 此布局非常适用于以紧凑形式显示大量信息。

![折叠布局](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

您可以使用[折叠组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表单中添加折叠布局。 有关如何配置折叠组件的各种属性的详细说明，请参阅[折叠组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)文章。

### 如何选择正确的布局？

选择正确的布局以优化用户体验和表单功能很重要。 该表可帮助您了解可用的各种布局选项，并指导您根据特定需求和用例选择最合适的布局：

| 专题 | 面板布局 | 向导布局 | 可折叠项布局 |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **目的** | 将相关内容分组为不同的部分 | 指导用户完成多步骤流程或表单 | 将内容整理到可折叠部分中 |
| **结构** | 不同的部分 | 连续步骤/页面 | 可折叠面板/区域 |
| **导航** | 单击面板标题以进行导航 |  — 前进：“下一步”按钮<br> — 后退：“后退”按钮<br> — 可选跳过步骤 | 单击标题可展开/折叠部分 |
| **用户体验** | 以可管理的方式组织大量内容 | 逐步指导，减少负担 | 具有展开/折叠部分的紧凑视图 |
| **用例** | 具有已分类分区的复杂表单 | 设置流程，复杂表单 | 常见问题解答、设置菜单、详细内容部分 |

## 另请参阅

{{universal-editor-see-also}}
