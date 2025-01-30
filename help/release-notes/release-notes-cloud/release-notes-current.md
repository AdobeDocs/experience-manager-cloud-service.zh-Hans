---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75a011ed952e1801f0988942d4501a52d348bb3f
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 44%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.1.0)的发布日期是2025年1月30日。 下一个功能版本(2025.2.0)计划于2025年2月27日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**内容片段编辑器评论功能现已正式可用**

在创作AEM内容片段时，通过在AEM内容片段编辑器中使用新的现代化注释服务轻松地与同事协作。
[了解详情](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**内容片段编辑器和管理员用户界面，更新了AEM as a Cloud Service版本支持**

新内容片段管理和编辑器用户界面支持的最低AEM as a Cloud Service版本现在为2023.8.13099。不再支持在正式发布新用户界面之前发布的早期版本

### 早期采用者计划 {#sites-early-adopter}

**增强的内容片段**

使用基于唯一ID的引用增强了[内容片段引用](/help/headless/graphql-api/uuid-reference-upgrade.md)，从而确保即使在移动资产或片段时也能保持稳定的链接，而无需更新或重新发布。 当前限制：页面引用尚不支持唯一 ID。如果在内容片段中引用页面，则不应使用此功能。

**用于内容片段投放的 AEM REST OpenAPI**

用于内容片段投放的[AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md)现在可用于AEM as a Cloud Service。

### 已弃用功能 {#sites-deprecated}

#### SPA编辑器 {#spa-editor}

[从2025.1.0版开始的新项目已弃用SPA编辑器](/help/implementing/developing/hybrid/introduction.md)。现有项目仍支持SPA编辑器，但不应将其用于新项目。

现在，在AEM中管理Headless内容的首选编辑器包括：

* [用于可视化编辑的通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)。
* [用于基于表单的编辑的内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)。

#### PWA功能 {#pwa-features}

[从2025.1.0版开始的新项目现已弃用AEM Sites的渐进式Web应用程序(PWA)功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。现有项目仍支持此功能，但不应用于新项目

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets中的新增功能 {#new-features-assets}

**Dynamic Media模板**

通过将URL嵌入任何第一方或第三方应用程序，使用易于使用的WYSIWYG Dynamic Media模板编辑器即时个性化图像和文本横幅，通过实时横幅内容更新推动高度引人入胜的体验。

![动态演绎](/help/assets/assets/dm-templates-smart-text-resize.png)

**Dynamic Media传递报告**

获得通过Dynamic Media交付的资产交付见解，包括资产级交付计数、反向链接详细信息、AEM Assets中的资产路径和唯一资产ID。 为AEM Assets存储库或特定文件夹层次结构中的所有资源生成报表。 通过这些洞察，您可以衡量已交付资产的ROI、评估渠道绩效并做出明智的资产管理决策。

![动态演绎](/help/assets/assets/referrer.png)

**Dynamic Media多音频和字幕**

[在Dynamic Media中支持视频的多字幕和多音轨](/help/assets/dynamic-media/video.md#about-msma) — 您现在可以轻松地将多个字幕和多音轨添加到主视频中。 这项功能意味着您的视频可供全球受众访问。 您可以用多种语言为全球观众自定单一的、已发布的主视频，并遵守不同地区的可访问性指南。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

**通过HTTP支持的动态自适应流**

推出了面向 Dynamic Media 视频交付（已启用 CMAF）中的自适应流式处理的新协议（DASH – 基于 HTTP 的动态自适应流式处理）支持：

* 自适应流(DASH/HLS)确保更好的视频用户观看体验。

* DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用

**资源关系**

Assets视图现在支持在简化的资源详细信息面板中查看和编辑资源关系。 轻松将Source和派生等关系添加到内容，以便使用者可以更有效地查找相关主页内容。

**重新处理资源**

Assets视图现在支持重新处理文件夹中可用的资源。 您可以选择使用&#x200B;**完整流程**&#x200B;选项或使用高级选项，如默认预览呈现版本、元数据、后处理工作流和处理配置文件。

### AEM Assets中的抢先体验功能 {#early-access-features-assets}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。字幕由原始音频、任何其他音频曲目或视频属性页面的“字幕和音频”选项卡中提供的额外字幕生成。 由于支持60多种语言，因此在发布视频之前，可以审核和预览字幕。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

* **管理发布**：您可以使用“管理发布”工作流跨环境发布或取消发布表单，通常是从创作实例到发布和预览实例。 它允许用户以简化的方式发布、取消发布或计划内容的出版物。

* **[自动保存基于核心组件的自适应表单草稿](/help/forms/save-core-component-based-form-as-draft.md)**：用户现在可以享受自动保存功能，该功能可以自动将部分完成的表单保存为草稿。他们可以稍后返回同一设备或其他设备来完成填写。此功能通过减少表单放弃来提高组织的转化率，因为用户不需要从头开始填写表单。

* **[规则编辑器增强功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：对于基于核心组件的自适应Forms，您可以使用调用服务的输出填充下拉选项并设置可重复面板或单个面板。 此外，此输出可用于验证其他字段。

* **[使用面板布局中的导航按钮增强用户体验](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您现在可以向面板布局中添加水平选项卡、垂直选项卡、可折叠项或向导等导航按钮。这些按钮简化了面板之间的过渡，将注意力集中在所选面板上，从而增强了用户体验。


### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### [在自适应Forms中HTML电子邮件模板](/help/forms/html-email-templates-in-adaptive-forms.md)

自适应Forms允许您使用HTML电子邮件模板。 通过HTML电子邮件模板，您可以在提交表单时发送丰富、个性化且具有视觉吸引力的电子邮件。 这些电子邮件可使用表单数据自定义，并使用各种电子邮件标记（如图像和链接）进行增强。 通过自适应Forms，您可以上传包含HTML模板的文件或使用纯文本编辑器创建这些模板。

![HTML电子邮件模板](/help/forms/assets/html-email.png)

#### 增强的云存储支持：直接将PDF上传到Azure Blob Storage

AEM Forms Document Generation API现在支持将生成的PDF文档直接上传到Azure Blob Storage。 此增强功能可简化存储和检索，提高效率以及与云工作流的集成。

* **[文件附件的 Base64 编码字符串支持](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：基于核心组件的自适应表单中的文件附件组件现在包含一个选项，可以将附加文件作为 Base64 编码字符串提交。

>[!IMPORTANT]
>
> 有兴趣加入早期访问计划以体验任何有关 Forms 方面的创新技术吗？请从您的工作邮件发送一封电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中注明您感兴趣的功能列表。## CIF 加载项 {#cloud-services-cif}

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21支持 {#java21}

现在，您可以使用Java 21构建代码，其中包括新增功能（例如，交换语句的模式匹配、密封类）和性能改进；最近还支持Java 17构建。 有关配置步骤，包括更新Maven项目和库版本，请参阅[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)文章。

在检测到Java 17或21内部版本时，将自动部署性能更高的Java 21 **运行时**。 但是，我们还建议通过电子邮件发送[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)，选择为使用Java 11构建的环境使用Java 21运行时。 了解[Java 21运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **运行时**&#x200B;将逐步部署到&#x200B;**所有**&#x200B;环境（已使用Java 17或21构建的环境除外，这些环境已具有Java 21运行时），从2月的沙盒和开发/RDE开始，然后在4月暂存/生产。

### 沙盒程序支持配置管道 {#sandbox-config-pipelines}

沙盒程序现在支持配置管道，该管道可以在Cloud Manager中进行配置以部署在git中保留的yaml文件。

[了解有关](/help/operations/config-pipeline.md)配置管道的更多信息，这些管道允许配置CDN、日志转发和版本清除/审核日志清除维护任务。

### 基于 OpenAPI 的 API - 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的AEM as a Cloud Service API遵循OpenAPI规范，目标是保持一致、详细记录并便于用户使用。 需要身份验证的端点的凭据通过创建Adobe Developer Console项目生成。

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。

* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和资产文件夹 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [ Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。如果您发现这项技术对AEM Publish交付和Edge Delivery Services项目很有用，Adobe将很乐意听到。 此外，请告知我们您打算将它用作产品路线图的输入内容。 请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

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
