---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 7c65208b948345ea185032a04595ffe65e95876d
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 99%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本（2025.1.0）的发布日期为 2025 年 1 月 30 日。下一个功能版本 (2025.2.0) 计划于 2025 年 2 月 27 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**内容片段编辑器评论功能现已正式推出**

通过使用 AEM 内容片段编辑器中的全新现代化评论服务，可以在创作 AEM 内容片段时轻松与同事协作。
[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**内容片段编辑器和管理用户界面，更新的 AEM as a Cloud Service 版本支持**

新的内容片段管理员和编辑器用户界面支持的最低 AEM as a Cloud Service 现在为 2023.8.13099。新用户界面正式发布之前的早期版本不再受支持

### 早期采用者计划 {#sites-early-adopter}

**增强内容片段**

[通过基于唯一 ID 的引用增强内容片段引用功能](/help/headless/graphql-api/uuid-reference-upgrade.md)，即使片段被移动到其他位置，也能帮助确保针对个体内容片段的 GraphQL 查询保持稳定。现在可以使用 “ByID” 查询。路径会发生更改，可能会破坏 “ByPath” 查询，但 UUID 是稳定的。新的 ID 还可以在任何查询或其他适用的 API 请求中作为属性返回。当前限制（2025.1）：页面引用尚不支持唯一 ID。如果在内容片段中引用页面，则不应使用此功能。该限制计划在下一个 AEM as a Cloud Service 版本中移除。

**用于内容片段投放的 AEM REST OpenAPI**

[用于内容片段投放的 AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) 现可用于 AEM as a Cloud Service。

### 已弃用功能 {#sites-deprecated}

#### SPA 编辑器 {#spa-editor}

从版本 2025.1.0 开始，[SPA 编辑器](/help/implementing/developing/hybrid/introduction.md)已在新项目中弃用。SPA 编辑器仍支持现有项目，但不应在新项目中使用。

现在管理 AEM 中的 Headless 内容时首选以下编辑器：

* [通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)，用于可视化编辑。
* [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。

#### PWA 功能 {#pwa-features}

从版本 2025.1.0 开始，AEM Sites 的[渐进式 Web 应用程序（PWA）功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)已在新项目中弃用。此功能仍支持现有项目，但不应在新项目中使用

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新增功能 {#new-features-assets}

**Dynamic Media 模板**

通过在任何第一方或第三方应用程序中嵌入 URL，使用简单易用的所见即所得 Dynamic Media 模板编辑器即时个性化图像和文本横幅，通过实时横幅内容更新推动极具吸引力的体验。

![动态演绎](/help/assets/assets/dm-templates-smart-text-resize.png)

**Dynamic Media 投放报告**

获取通过 Dynamic Media 投放资产的投放洞察，包括资产级别投放计数、反向链接详细信息、AEM Assets 中的资产路径和唯一资产 ID。为 AEM Assets 存储库或特定文件夹层次结构中的所有资产生成报告。通过这些洞察，您可以衡量已投放资产的 ROI，评估渠道性能，并为资产管理做出明智决策。

![动态演绎](/help/assets/assets/referrer.png)

**Dynamic Media 多音频和字幕**

[Dynamic Media 中的视频支持多字幕和多音轨](/help/assets/dynamic-media/video.md#about-msma)，现在可轻松地将多个字幕和多个音轨添加到主视频。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

**基于 HTTP 支持的动态自适应流式处理**

推出了面向 Dynamic Media 视频交付（已启用 CMAF）中的自适应流式处理的新协议（DASH – 基于 HTTP 的动态自适应流式处理）支持：

* 自适应流式处理（DASH/HLS）确保改善用户对视频的观看体验。

* DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用

**资产关系**

资产视图现在支持在简化的资产详细信息面板中查看和编辑资产关系。在内容中轻松添加来源和衍生等关系，以便用户可以更有效地找到相关的主要内容。

**重新处理资产**

资产视图现在支持重新处理文件夹中可用的资产。您可以选择使用&#x200B;**完整流程**&#x200B;选项，也可以使用高级选项，例如默认预览演绎版、元数据、后期处理工作流和资产处理配置文件。

### AEM Assets 中的早期访问功能 {#early-access-features-assets}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。字幕是根据原始音频、任何附加音轨或视频属性页面“字幕和音频”选项卡中提供的额外字幕生成的。支持超过 60 种语言，可以在发布视频之前查看和预览字幕。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

#### 管理发布

您可以使用“管理发布”工作流跨环境发布或取消发布表单，通常是从作者实例到发布和预览实例。它允许用户以简化的方式发布、取消发布或计划内容的发布。

#### 自动保存基于核心组件的自适应表单草稿

用户现在可以享受[自动保存功能](/help/forms/save-core-component-based-form-as-draft.md)，该功能可以自动将部分完成的表单保存为草稿。他们可以稍后返回同一设备或其他设备来完成填写。此功能通过减少表单放弃来提高组织的转化率，因为用户不需要从头开始填写表单。

#### 规则编辑器增强功能

对于基于核心组件的自适应表单，您可以使用[调用服务的输出来填充下拉选项，并设置可重复或单个面板](/help/forms/invoke-service-enhancements-rule-editor.md)。此外，此输出可用于验证其他字段。

#### 使用面板布局中的导航按钮增强用户体验

您现在可以向面板布局添加导航按钮，例如水平选项卡、垂直选项卡、可折叠项或向导。这些按钮[简化了面板之间的过渡，将注意力集中在所选面板上，从而增强了用户体验](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)。


### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 自适应表单中的 HTML 电子邮件模板

自适应表单允许您使用 [HTML 电子邮件模板](/help/forms/html-email-templates-in-adaptive-forms.md)。HTML 电子邮件模板可让您在提交表单时发送内容丰富、个性化且具有视觉吸引力的电子邮件。这些电子邮件可使用表单数据进行自定义，并使用各种电子邮件标记（如图像和链接）进行增强。使用自适应表单，您可以上传包含 HTML 模板的文件，也可以使用纯文本编辑器来创建这些模板。

![HTML 电子邮件模板](/help/forms/assets/html-email.png)

#### 增强的云存储支持：将 PDF 直接上传至 Azure Blob 存储

AEM Forms 文档生成 API 现在允许您[直接将生成的 PDF 文档上传到 Azure Blob 存储](/help/forms/early-access-ea-features.md#doc-generation-api)。这种增强功能简化了存储和检索，提高了效率并与云工作流进行集成。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21 支持 {#java21}

您现在可以使用 Java 21 构建代码，其中包括新功能（如切换语句的模式匹配、密封类）和性能改进。Java 17 构建也获得了新的支持。有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 构建时，将自动部署性能更高的 Java 21 **运行时**。不过，我们也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [ Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **运行时**&#x200B;将逐步部署到&#x200B;**所有**&#x200B;环境（已使用 Java 17 或 21 构建的环境除外，这些环境已经有了 Java 21 运行时），二月份将从沙盒和开发/RDE 开始，然后在四月份部署到阶段/生产环境。

### 沙盒程序支持配置管道 {#sandbox-config-pipelines}

沙盒程序现在支持配置管道，可以在 Cloud Manager 中进行配置，以部署在 Git 中持久保存的 yaml 文件。

[了解更多](/help/operations/config-pipeline.md)关于配置管道的信息，它可以完成配置 CDN、日志转发和版本清除/审核日志清除维护的任务。

### 基于 OpenAPI 的 API - 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。创建 Adobe Developer Console 项目时生成需要身份验证端点的凭据。

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。

* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和资产文件夹 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [ Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。Adobe 希望了解您是否认为这项技术对 AEM Publish Delivery 和 Edge Delivery Services 项目有用。此外，请告诉我们您设想将其用于哪些用途，以便为产品路线图提供意见。请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎您的反馈，可以将意见通过电子邮件发送至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[此处](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-0-release/whats-new-2024-10-0)找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表。

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
