---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 83bc4e09cc7b6c420eee64091fab773ee1dcbd85
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 39%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2024.11.0)的发布日期是2024年11月21日。 下一个功能版本(2024.12.0)计划于2024年12月12日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

通过通用编辑器创作&#x200B;**[!DNL Edge Delivery Services]页面模板**

将任何Edge Delivery页面快速转换为页面模板。 这允许您启动具有预定义结构和内容的新页面，而不是空白页面。 [阅读更多](/help/sites-cloud/authoring/universal-editor/templates.md)。

**[!DNL Edge Delivery Services]CSV导入程序用于通过AEM实例发布**

在您喜爱的电子表格工具中高效地管理Edge Delivery电子表格数据（例如重定向），并通过新的CSV导入器将其上传到AEM。 [阅读更多](/help/edge/wysiwyg-authoring/tabular-data.md#importing)。

### AEM Sites中的预发行版功能

使用基于唯一ID的引用增强了[内容片段引用](/help/headless/graphql-api/uuid-reference-upgrade.md)，从而确保即使在移动资产或片段时仍保持有效的稳定链接 — 无需更新或重新发布。 当前限制：唯一ID尚不支持页面引用。 如果页面在内容片段中被引用，则不应使用此功能。

### 早期采用者计划 {#sites-early-adopter}

**用于内容片段投放的 AEM REST OpenAPI**

[用于内容片段投放的 AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) 现已提供给 AEM AEM as a Cloud Service 使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media中的抢先体验功能 {#dm-early-access}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。AI 会分析视频的音轨以转录语音并创建字幕，这些字幕可以进行编辑，以提高准确性或实现定制化。这些字幕有助于满足可访问性要求，并提高依赖或偏好基于文本的视频支持服务的观众的视频参与度。

为了尽早获得 Dynamic Media 帐户上 AI 生成的字幕支持，[请创建并提交 Adobe 客户支持案例](/help/assets/dynamic-media/video.md##enable-dash)。

**Dynamic Media传递报告**

通过Dynamic Media提供的资产、资产级别投放计数、反向链接信息、AEM Assets中的资产路径和唯一资产ID，获得资产投放见解。 可以为AEM Assets存储库中通过Dynamic Media交付的所有资源或AEM Assets中的特定文件夹层次结构生成报表。 分析有助于衡量所交付资产的ROI、衡量渠道绩效并帮助制定针对资产的明智资产管理任务。

若要提前访问您Dynamic Media帐户的Dynamic Media交付报告，请[创建并提交Adobe的客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。

### 资源视图中的新增功能 {#assets-view-new-features}

**Dynamic Media面板**

通过Assets视图，您现在可以从提供给您的单独面板中使用OpenAPI演绎版访问Dynamic Media和Dynamic Media。 您可以选择复制投放URL，或根据资源和演绎版类型下载演绎版。 有关详细信息，请参阅具有OpenAPI功能的[Dynamic Media呈现](/help/assets/renditions.md#dynamic-media-renditions)和[Dynamic Media](/help/assets/renditions.md#dm-with-openapi-renditions)。

![动态呈现版本](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

* **[轻松更新 Adobe Sign 范围](/help/forms/adobe-sign-integration-adaptive-forms.md)**：您可以直接从 AEM 云配置页面修改 Adobe Sign 配置的范围，从而更快、更轻松地更新现有配置。

* **[自适应表单的异步函数支持](/help/forms/using-async-funct-in-rule-editor.md)**：当您的自适应表单需要异步操作（例如等待外部流程或数据检索）时，可以使用自定义函数实施这些操作，并在规则编辑器中对其进行配置。

### AEM Forms中的预发行功能 {#forms-new-prerelease-features}

* **管理发布**：您可以使用管理发布工作流跨环境发布或取消发布表单，通常是从创作实例到发布和预览实例。 它允许用户以简化的方式发布、取消发布或计划内容发布。

* **[自动保存基于核心组件的自适应表单草稿](/help/forms/save-core-component-based-form-as-draft.md)**：用户现在可以享受自动保存功能，该功能可以自动将部分完成的表单保存为草稿。他们可以稍后返回同一设备或其他设备来完成填写。此功能通过减少表单放弃来提高组织的转化率，因为用户不需要从头开始填写表单。

* **[规则编辑器增强功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：对于基于核心组件的自适应Forms，现在可以使用“调用服务”的输出填充下拉选项，使用“调用服务”的输出设置可重复的面板，使用“调用服务”的输出设置各个面板，以及使用“调用服务”的输出参数验证其他字段。

* **[使用面板布局中的导航按钮增强用户体验](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您现在可以向面板布局中添加水平选项卡、垂直选项卡、可折叠项或向导等导航按钮。这些按钮简化了面板之间的过渡，将注意力集中在所选面板上，从而增强了用户体验。


### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 集成

* **[将自适应Forms与Adobe Marketo Engage集成](/help/forms/integrate-form-to-marketo-engage.md)**： AEM Formsas a Cloud Service现在包含一个易于使用的选项，用于将自适应Forms与Adobe Marketo Engage连接。 通过此集成，您可以使用Marketo Engage的潜在客户捕获和相关自定义对象直接创建自适应Forms。 您现在可以使用Marketo Engage中的数据预填表单字段，并将其提交回以自动化智能营销活动和电子邮件自动化等工作流。 您还可以将自适应表单与Munchkin库连接起来，以跟踪访问次数、点击次数和表单提交次数。

#### 自适应Forms和HTML5 Forms

* **[基于现有XFA模板创建自适应Forms](/help/forms/create-adaptive-form-using-xfa-templates.md)**：您现在可以使用XFA表单模板（*.XDP文件）创建基于核心组件的自适应Forms。 此功能有助于那些已在XFA技术方面进行了现有投资的AEM Forms内部部署客户采用AEM Formsas a Cloud Service。

* **HTML5 Forms（基于XFA的Web窗体）**：现在，使用XFA技术的AEM Forms本地客户可以轻松过渡到AEM Formsas a Cloud Service，同时保留他们现有的使用HTML5 Forms（基于XFA的Web窗体）的用户体验。 此功能支持以HTML5格式呈现XFA表单模板，使得在不支持基于XFA的PDF forms上可访问表单。

  ![HTMLForms（基于XFA的Web窗体）](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[文件附件的Base64编码字符串支持](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：基于核心组件的自适应Forms中的文件附件组件现在包含一个选项，可用于将附加文件作为Base64编码字符串提交。

#### 交互式通信和通信API

* **交互式通信编辑器**：交互式通信编辑器是一种用户友好的图形化通信设计工具，它简化了个性化数据驱动通信的创建，并在任何现代浏览器中运行。 它支持无缝的数据集成、复杂的逻辑定义以及富媒体集成，从而确保针对各种业务需求生成专业且合规的文档、通信和模板。

  ![交互式通信编辑器](/help/forms/assets/ic-editor.png)


* **[PDF/A合规性增强功能](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：您现在可以使用通信API将PDF文档转换为PDF/A格式(1a、2a、3a)以进行存档，同时确保可访问性并验证是否符合这些标准。


* **[签名API (Document Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**：通信API中新的RESTful API可轻松管理PDF签名。 它支持如下操作：
   * 清除签名：从指定字段中删除签名。
   * 删除签名字段：删除指定的签名字段。


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自动化表单转换服务

* **[将PDF forms转换为基于核心组件的自适应Forms](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**：您现在可以使用Automated forms conversion服务将PDF forms、AcroForms或基于XFA的表单转换为基于核心组件的自适应Forms。


>[!IMPORTANT]
>
> 有兴趣加入早期访问计划以体验任何有关表单方面的创新技术吗？请从您的工作邮件发送一封电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中注明您感兴趣的功能列表。## CIF加载项{#cloud-services-cif}

## CIF 加载项 {#cif}

### 错误修复 {#bug-fixes-cif}

* 修复了 UI 测试以便与 Core CIF 组件正常配合使用。
* 解决了类别 URL 格式在云实例中无法按预期运行的问题。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 提高了树复制性能(并弃用Publish内容树工作流) {#tree-replication-performance}

[树激活工作流步骤](/help/operations/replication.md#tree-activation)是用于复制深层内容层次结构的新工作流模型步骤。 请注意，它允许独立复制（例如，通过快速发布或管理发布）与正在进行的树复制工作流并行进行。 如果您需要在批量复制仍在进行时发布一些时效性强的内容，此功能会特别有用。 树复制步骤取代了Publish内容树工作流及其相关的工作流步骤，这些步骤现已弃用。

### 基于OpenAPI的API — 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将AEM作为Cloud Service功能深入集成到他们自己的应用程序和工具中。 新的AEM as a Cloud Service API将遵循OpenAPI规范，目标是保持一致、详细记录并便于用户使用。 需要身份验证的端点的凭据将通过创建Adobe Developer Console项目生成。

了解有关[基于OpenAPI的AEM API](/help/implementing/developing/open-api-based-apis.md)的详细信息，并尝试使用说明配置和使用情况的[端到端教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具体而言，下面列出的API端点作为率先采用者计划的一部分提供。 如有兴趣，请发送电子邮件至[aem-apis@adobe.com](mailto:aem-apis@adobe.com)，说明您打算如何使用它们。
* [站点内容片段API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [站点和Assets文件夹API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge计算 — 请求反馈！ {#edge-computing-feedback}

Edge计算使数据处理更接近浏览器，其优势包括减少延迟。 作为路线图中的投入，我们希望了解您是否认为这项技术对AEM Publish交付和Edge Delivery Services项目非常有用，以及您设想将其用于什么用途。 向[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)发送电子邮件，其中包含问题和评论！

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe欢迎反馈，您可以通过电子邮件将其发送至[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

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
