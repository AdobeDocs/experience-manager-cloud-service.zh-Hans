---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d7156a79f004a454b7689b2085a97d4c513d52b7
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2022 版或 2023 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前功能版本 (2024.11.0) 的发布日期为 2024 年 11 月 21 日。下一个功能版本(2025.1.0)计划于2024年1月30日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2024 年 11 月版概述视频可了解在 2024.11.0 版中添加的功能的概要：

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]具有通用编辑器创作功能的页面模板**

快速将任何 Edge Delivery 页面转换为页面模板。这样就可以用预定义的结构和内容启动新页面，而不是空白页面。[了解详情](/help/sites-cloud/authoring/universal-editor/templates.md)。

**[!DNL Edge Delivery Services]用于通过 AEM 实例发布的 CSV 导入程序**

在您最喜欢的电子表格工具中有效地管理 Edge Delivery 电子表格数据（例如重定向），并通过新的 CSV 导入程序将其上传到 AEM。[了解详情](/help/edge/wysiwyg-authoring/tabular-data.md#importing)。

### AEM Sites 中的预发行功能

增强[内容片段引用功能，使用基于唯一 ID 的引用](/help/headless/graphql-api/uuid-reference-upgrade.md)，确保即使资产或片段被移动，链接仍然稳定有效，无需更新或重新发布。当前限制：页面引用尚不支持唯一 ID。如果在内容片段中引用页面，则不应使用此功能。

### 早期采用者计划 {#sites-early-adopter}

**用于内容片段投放的 AEM REST OpenAPI**

[用于内容片段投放的 AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) 现已提供给 AEM as a Cloud Service 使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 中的早期访问功能 {#dm-early-access}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。AI 会分析视频的音轨以转录语音并创建字幕，这些字幕可以进行编辑，以提高准确性或实现定制化。这些字幕有助于满足可访问性要求，并提高依赖或偏好基于文本的视频支持服务的观众的视频参与度。

为了尽早获得 Dynamic Media 帐户上 AI 生成的字幕支持，[请创建并提交 Adobe 客户支持案例](/help/assets/dynamic-media/video.md##enable-dash)。

**Dynamic Media 投放报告**

获取通过 Dynamic Media 投放资产的投放洞察，包括资产级别投放计数、推荐人信息、AEM Assets 中的资产路径和唯一资产 ID。可针对通过 AEM Assets 存储库 Dynamic Media 投放的所有资产或 AEM Assets 中的特定文件夹层级生成报告。Insights 有助于衡量投放资产的 ROI、衡量渠道性能，并有助于对资产采取明智的资产管理任务。

为了尽早获得 Dynamic Media 帐户上的 Dynamic Media 投放报告，[请创建并提交 Adobe 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。

### Assets 视图中的新增功能 {#assets-view-new-features}

**Dynamic Media 面板**

现在，您可以通过 Assets 视图从单独的面板访问 Dynamic Media 和具有 OpenAPI 演绎的 Dynamic Media。您可以选择复制投放 URL 或根据资产和演绎类型下载演绎。有关详细信息，请参阅 [Dynamic Media 演绎](/help/assets/renditions.md#dynamic-media-renditions)和[具有 OpenAPI 功能的 Dynamic Media 演绎](/help/assets/renditions.md#dm-with-openapi-renditions)。

![动态演绎](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

* **[轻松更新 Adobe Sign 范围](/help/forms/adobe-sign-integration-adaptive-forms.md)**：您可以直接从 AEM 云配置页面修改 Adobe Sign 配置的范围，从而更快、更轻松地更新现有配置。

* **[自适应表单的异步函数支持](/help/forms/using-async-funct-in-rule-editor.md)**：当您的自适应表单需要异步操作（例如等待外部流程或数据检索）时，可以使用自定义函数实施这些操作，并在规则编辑器中对其进行配置。

### AEM Forms 中的预发行版功能 {#forms-new-prerelease-features}

* **管理出版物**：您可以使用管理出版物工作流跨环境发布或取消发布表单，通常是从作者实例到发布和预览实例。它允许用户以简化的方式发布、取消发布或计划内容的出版物。

* **[自动保存基于核心组件的自适应表单草稿](/help/forms/save-core-component-based-form-as-draft.md)**：用户现在可以享受自动保存功能，该功能可以自动将部分完成的表单保存为草稿。他们可以稍后返回同一设备或其他设备来完成填写。此功能通过减少表单放弃来提高组织的转化率，因为用户不需要从头开始填写表单。

* **[规则编辑器增强功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：对于基于核心组件的自适应表单，您现在可以使用调用服务的输出填充下拉选项，使用调用服务的输出设置可重复面板，使用调用服务的输出设置单个面板，并使用调用服务的输出参数来验证其他字段。

* **[使用面板布局中的导航按钮增强用户体验](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您现在可以向面板布局中添加水平选项卡、垂直选项卡、可折叠项或向导等导航按钮。这些按钮简化了面板之间的过渡，将注意力集中在所选面板上，从而增强了用户体验。


### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 集成

* **[将自适应表单与 Adobe Marketo Engage 集成](/help/forms/integrate-form-to-marketo-engage.md)**：AEM Forms as a Cloud Service 现在包含一个易于使用的选项，用于将自适应表单与 Adobe Marketo Engage 连接起来。通过此集成，您可以直接使用 Marketo Engage 的商机捕获和相关的自定义对象创建自适应表单。您现在可以使用来自 Marketo Engage 的数据预填充表单字段，并提交数据以实现智能营销活动和电子邮件自动化等工作流程的自动化。您还可以将自适应表单 与 Munchkin 库连接起来，跟踪访问次数、点击次数和表单提交次数。

#### 自适应表单和 HTML5 表单

* **[基于现有 XFA 模板创建自适应表单](/help/forms/create-adaptive-form-using-xfa-templates.md)**：您现在可以使用 XFA 表单模板（*.XDP 文件）创建基于核心组件的自适应表单。此功能可帮助已在 XFA 技术上进行投资的 AEM Forms 内部部署客户使用 AEM Forms as a Cloud Service。

* **HTML5 表单（基于 XFA 的网页表单）**：现在，使用 XFA 技术的 AEM Forms 内部部署客户可以轻松过渡到 AEM Forms as a Cloud Service，同时保留他们现有的 HTML5 表单（基于 XFA 的网页表单）用户体验。此功能支持以 HTML5 格式渲染的 XFA 表单模板，使得表单可在那些不支持基于 XFA 的 PDF 表单的设备上访问。

  ![HTML 表单（基于 XFA 的网页表单）](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[文件附件的 Base64 编码字符串支持](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：基于核心组件的自适应表单中的文件附件组件现在包含一个选项，可以将附加文件作为 Base64 编码字符串提交。

#### 交互式通信和通信 API

* **交互式通信编辑器**：交互式通信编辑器是一种用户友好的图形通信设计工具，可简化个性化数据驱动通信的创建，并可在任何现代浏览器中运行。它支持无缝数据集成、复杂逻辑定义和富媒体集成，确保满足各种业务需求的专业、合规的文档、通信和模板生成。

  ![交互式通信编辑器](/help/forms/assets/ic-editor.png)


* **[PDF/A 合规性增强](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：您现在可以使用通信 API 将 PDF 文档转换为 PDF/A 格式（1a、2a、3a）以供存档，同时确保可访问性并验证是否符合这些标准。


* **[签名 API（Document Assurance）](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**：通信 API 中新的 RESTful API，支持轻松管理 PDF 签名。它支持如下操作：
   * 清除签名：从指定字段中移除签名。
   * 移除签名字段：删除指定的签名字段。


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自动化表单转换服务

* **[将 PDF 表单转换为基于核心组件的自适应表单](https://experienceleague.adobe.com/zh-hans/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**：您现在可以使用自动表单转换服务将 PDF 表单 、AcroForms 或基于 XFA 的表单转换为基于核心组件的自适应表单。


>[!IMPORTANT]
>
> 有兴趣加入早期访问计划以体验任何有关 Forms 方面的创新技术吗？请从您的工作邮件发送一封电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中注明您感兴趣的功能列表。## CIF 加载项 {#cloud-services-cif}

## CIF 加载项 {#cif}

### 错误修复 {#bug-fixes-cif}

* 修复了 UI 测试以便与 Core CIF 组件正常配合使用。
* 解决了类别 URL 格式在云实例中无法按预期运行的问题。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 改进树复制性能（并弃用发布内容树工作流） {#tree-replication-performance}

[树激活工作流步骤](/help/operations/replication.md#tree-activation)是推荐用于复制深度内容层次结构的新的工作流模型步骤。值得注意的是，它允许独立复制（例如，通过快速发布或管理出版物）与正在进行的树复制工作流并行进行。如果您需要在批量复制仍在进行时发布一些时效性较强的内容，该工具尤其有用。树复制步骤替换了发布内容树工作流及其相关的工作流步骤，后者现在已被弃用。

### 基于 OpenAPI 的 API - 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 将遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。创建 Adobe Developer Console 项目时将生成需要身份验证端点的凭据。

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。
* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和资产文件夹 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [ Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。作为对路线图的投入，我们希望了解您是否认为这项技术对 AEM Publish Delivery 和 Edge Delivery Services 项目有用，以及您设想将其用于哪些用途。请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎您的反馈，可以将意见通过电子邮件发送至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## 通用编辑器 {#universal-editor}

您可以在[此处](/help/release-notes/universal-editor/current.md)找到通用编辑器版本的完整列表。

## 生成变体 {#generate-variations}

您可以在[此处](/help/generative-ai/release-notes-generate-variations.md)找到生成变体版本的完整列表。

## Experience Cloud 发行说明 {#experience-cloud}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/release-notes/experience-cloud/current)找到有关其他 Experience Cloud 应用程序版本的信息。
