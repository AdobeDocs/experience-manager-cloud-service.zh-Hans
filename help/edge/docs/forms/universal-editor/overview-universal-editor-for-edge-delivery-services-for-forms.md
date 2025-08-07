---
title: Edge Delivery Services for Forms通用编辑器
description: 使用 Edge Delivery Services for Forms通用编辑器创建自适应表单。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 100%

---


# Edge Delivery Services for Forms通用编辑器

通用编辑器通过提供简单、可视和直观的所见即所得（WYSIWYG）界面，彻底改变了 Adobe Edge Delivery Services 的表单创建方式。它专为内容创建者和表单作者设计，消除了传统表单构建流程的复杂性，使非技术用户也能使用。

使用通用编辑器，您可以使用预建组件（如文本字段、复选框和单选按钮）快速设计响应式交互表单。其强大的功能集支持动态规则、无缝数据集成和高级个性化，确保每个表单都符合您的需求。

无论您是要管理轻量级客户端渲染、确保跨浏览器兼容性，还是要遵守严格的可访问性标准，通用编辑器都能为创建和管理表单提供简化的解决方案。

![通用编辑器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Edge Delivery Services for Forms通用编辑器的主要功能



| ![所见即所得界面](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![规则编辑器](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![提交操作](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**所见即所得界面**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**规则编辑器**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**提交操作**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| 通用编辑器为表单设计提供了所见即所得的界面，具有预建组件库、响应式设计、基于模板的创建和实时字段修改。 | 规则编辑器允许用户使用事件驱动规则、即时验证和通过轻量级 JavaScript 和 JSON 进行错误处理来创建动态表单交互。 | 提交操作支持后端集成、条件提交逻辑、安全端点和预处理器，简化提交工作流程。 |

| ![发布/取消发布](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![响应式模式](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![自定义组件](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**发布/取消发布**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**响应式模式**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**自定义组件**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| 轻松控制表单的可见性——只需单击几下即可直接从编辑器发布或取消发布表单。 | 设计可跨设备（台式机、平板电脑和移动设备）无缝适应的表单。使用响应式模式预览和测试各种屏幕尺寸的表单。 | 自定义组件允许开发人员通过创建针对特定组织用例定制的独特元素来扩展表单功能。 |

| ![样式](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![预填服务](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B 测试](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**样式**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **预填服务**（即将推出） | [**A/B 测试**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| 使用 CSS 样式使开发人员能够自定义表单元素的外观，并创建与网站美学相符的在视觉上富有吸引力的设计。 | 预填服务会自动使用来自各种来源的相关用户数据填充表单字段，从而减少手动输入并增强用户体验。 | A/B 测试使组织能够尝试不同的表单设计、布局和功能，以确定性能最佳的变体。 |

| ![分析与跟踪](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![表单片段](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![数据绑定](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**分析与跟踪**](https://www.aem.live/developer/martech-integration) | **表单片段**（即将推出） | [**数据绑定**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| 通过内置分析和跟踪功能深入了解用户行为、表单交互和提交率，从而实现数据驱动的表单优化。 | 表单片段通过允许创建一次常用的部分并在多个表单中重复使用来实现可重用性，从而确保一致性并减少维护工作量。 | 数据绑定实现了表单字段和后端数据源的直接连接，从而支持实时更新和高级数据映射。 |

| ![验证码](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![嵌入表单](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![谢谢配置](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**验证码**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **嵌入表单**（即将推出） | [**谢谢配置**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| 使用 reCAPTCHA 来保护表单免受自动机器人的攻击，从而确保数据收集安全可靠。 | 使用通用编辑器的内置嵌入组件将表单直接嵌入到 Edge Delivery Services Sites。 | 轻松地自定义成功提交表单后向用户显示的确认信息或页面。 |



## 预建表单组件

通用编辑器提供以下现成的表单组件：

<table>
  <thead>
    <tr>
      <th></th> 
      <th>表单组件</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="表单组件" style="width: 100%;"></td> 
      <td><b>可折叠项</b></td>
      <td>用于组织内容的可折叠面板结构。</td>
    </tr>
    <tr>
      <td><b>按钮</b></td>
      <td>为导航或自定义逻辑等操作添加交互式元素。</td>
    </tr>
    <tr>
      <td><b>验证码</b></td>
      <td>要求用户使用 Google reCaptcha 或 HCaptcha 完成人工验证任务，从而防止垃圾邮件。</td>
    </tr>
    <tr>
      <td><b>复选框</b></td>
      <td>允许用户配置复选框。</td>
    </tr>
    <tr>
      <td><b>复选框组</b></td>
      <td>允许用户从一个组中选择多个选项。</td>
    </tr>
    <tr>
      <td><b>日期选取器</b></td>
      <td>允许用户使用日程表界面选择日期。</td>
    </tr>
    <tr>
      <td><b>下拉列表</b></td>
      <td>在预定义列表中提供单选或多选选项。</td>
    </tr>
    <tr>
      <td><b>电子邮件</b></td>
      <td>使用基本格式验证捕获电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>文件附件</b></td>
      <td>支持上传文档、图像或其他文件类型。</td>
    </tr>
    <tr>
      <td><b>表单片段</b></td>
      <td>可重复使用的表单组件，用于地址字段或联系详细信息等部分。</td>
    </tr>
    <tr>
      <td><b>图像</b></td>
      <td>支持在表单内上传和显示图像。</td>
    </tr>
    <tr>
      <td><b>模态</b></td>
      <td>显示弹出窗口对话框，通常用于警告、附加信息或确认。</td>
    </tr>
    <tr>
      <td><b>数值字段</b></td>
      <td>捕获数值输入，允许验证数字或范围。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可扩展/折叠面板来组织表单部分。</td>
    </tr>
    <tr>
      <td><b>单选按钮</b></td>
      <td>允许从一组选项中进行单选。</td>
    </tr>
    <tr>
      <td><b>评分</b></td>
      <td>允许用户提供星级评分。</td>
    </tr>
    <tr>
      <td><b>重置按钮</b></td>
      <td>将表单字段重置为其默认状态。</td>
    </tr>
    <tr>
      <td><b>提交按钮</b></td>
      <td>触发器表单提交并启动定义的工作流程。</td>
    </tr>
    <tr>
      <td><b>电话号码字段</b></td>
      <td>捕获基于国家/地区格式的电话号码。</td>
    </tr>
    <tr>
      <td><b>文本</b></td>
      <td>通过复选框提供一个专门用于显示法律条款和收集用户协议的分区。</td>
    </tr>
    <tr>
      <td><b>文本字段</b></td>
      <td>捕获单行输入，例如姓名或电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>向导</b></td>
      <td>指导用户逐步完成多部分表单流程。</td>
    </tr>
  </tbody>
</table>


## 入门培训

## 常见问题解答（FAQ）

**问：谁可以使用通用编辑器？**
通用编辑器专为广大用户设计，包括：

- 希望创建具有视觉吸引力表单的内容创建者。
- 需要高级自定义和集成功能的开发人员。
- 寻求可扩展、安全和合规表单解决方案的组织。

**问：可以把使用通用编辑器创建的表单集成到我现有的系统中吗？**
绝对可以。通用编辑器支持与后端系统的无缝数据绑定，实现实时更新和高级数据映射。它还与 Adobe Workfront 等工具集成，用于任务管理，并支持用于数据提交工作流的安全端点。

**问：可以自定义表单组件吗？**
可以，通用编辑器允许开发人员创建符合特定组织需求的自定义组件。此外，您还可以通过 UI 扩展和自定义工作流来扩展编辑器的功能。

**问：通用编辑器如何处理可访问性？**
通用编辑器的设计严格遵守可访问性标准，包括 WCAG（Web 内容无障碍准则）。这可确保残障人士也能使用表单，从而提供一种包容性的体验。

**问：可以从表单中获得哪些分析结果？**
通用编辑器包含内置分析和跟踪工具，可监测用户互动、表单提交率和转化量度。这些洞察有助于优化表单，提高性能。




