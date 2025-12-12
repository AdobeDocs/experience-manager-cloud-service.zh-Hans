---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 6d86413449dbde8566f0f653071a2f29ab9c13ab
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 62%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.12.0)的发布日期是2025年12月11日。 下一个功能版本(2026.1.0)计划于2026年1月29日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440930?captions=chi_hans&quality=12)

-->

## AEM中的代理 {#agents-in-aem}

AEM提供了一系列代理，使您能够加快内容创建并自动编排更改。 有关详细信息，请参阅[AEM代理概述](/help/ai-in-aem/agents/overview.md)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### AEM Forms 中新的早期访问功能 {#forms-new-early-access-features}

AEM Forms 早期访问计划为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

这些发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 交互式通信增强功能

##### 模板锁定

锁定模板中的内容和布局元素，以维护品牌完整性并防止未经授权的修改。 这可确保所有通信的设计一致性。

##### 内容溢出支持

为流式布局引入“允许在内容中使用分页符”选项。 此增强功能可顺利进行多页编辑，并更好地管理复杂文档的文本。

##### XDP文件编辑

交互式通信编辑器现在支持XDP编辑，包括片段集成。 您现在可以在浏览器中编辑XDP文件，而不是只在Forms Windows桌面上运行的Microsoft Designer。

##### 动态页面编号

在主页上自动显示“第#页，共##页”，以便跨多页文档进行清晰、一致的分页。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础 {#foundation}

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation的新功能 {#foundation-new}

#### 即将弃用 Java API {#java-api-deprecation}

若干已弃用的 API 于 8 月 31 日被标记为移除，因此不应再被引用。如果在代码中检测到已弃用的API，您将会收到操作中心通知，并且在1月29日之后，将在Cloud Manager构建期间显示通知，以强调删除使用情况的重要性。 请查看[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整详细信息。但为了方便起见，下面列出了这些 API：

+++ 展开查看 Java API 弃用项

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

#### Java 11 运行时弃用 {#java11-runtime-deprecation}

Adobe于2025年10月14日将&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;环境升级到更高性能的&#x200B;**Java 21运行时**。 从&#x200B;**1月下旬**&#x200B;开始，AEM Cloud Service SDK或任何云环境都不会使用Java 11运行时。

>[!NOTE]
>
> 要利用最新的性能优化和语言增强功能，建议使用Java 17或Java 21（首选）进行构建。 目前仍支持使用Java 8和Java 11进行构建，但将在即将发布的版本中弃用。 弃用之前，将单独发布通信。 请参阅&#x200B;*本文*&#x200B;的[生成时间要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)部分。
>

#### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从&#x200B;**1月29日**&#x200B;开始，将忽略任何不受支持的自定义日志记录覆盖。 根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation早期采用者功能 {#foundation-early-adopter}

#### 暂停自动维护更新 {#pause-updates}

上线日、直播活动、销售高峰——这些关键时刻绝不能出问题。[我们的新自助功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)可在关键时段阻止自动维护更新，确保您的团队专注无扰。

* 安静时段：在每天设定的时间内阻止自动维护更新。非常适合工作时段、夜间任务或早间切换。
* 无更新周期：阻止长达一周的自动维护更新。可用于产品发布、促销活动或年度冻结。

>[!NOTE]
>
>此功能自 9 月 25 日起作为有限可用性功能提供。
>请发送邮件至 [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) 以在您的项目中启用。
>

#### 边缘计算（Beta 计划） {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，重新设置响应的格式
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

#### Edge Delivery Services 的边缘身份验证（Beta 计划） {#edge-authentication}

边缘身份验证可让您将对 Edge Delivery Services 页面的访问限制为仅限已通过身份标识提供者 (IdP) 认证的用户。此功能通过部署 OpenID Connect (OIDC) 配置 YAML 文件来实现。

如有兴趣，请发送邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并简要说明您的用例及相关问题。

#### 金丝雀生产部署：在接受真实流量前测试代码（Beta 计划） {#canary-beta}

您可以在对最终用户开放前，先使用仅限内部的测试流量验证生产构建。将构建部署到生产环境，仅通过特殊标头路由金丝雀流量，监控行为，然后再决定是否提升为真实流量或回滚——而不会影响客户。

您可以将代码发布部署到生产环境，但在决定接受真实流量或回滚之前，仅将其限制在内部测试流量中。

如需申请访问权限并分享反馈，请发送邮件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com)。


#### 人工智能答案 — 适用于AEM Sites (Beta程序)的更智能、上下文感知响应 {#ai-answers-beta}

人工智能解答为访客引入了一种与内容交互的新方法。 它通过检索 — 增强型生成(RAG)技术提供支持，利用您的AEM管理的数据直接在您的数字体验中提供准确、品牌一致的答案。

我们正准备启动AI Answers Beta计划，现在正在邀请客户注册其兴趣。 由于Beta版的容量非常有限，因此早期注册将得到优先考虑。 参与测试版将允许您在AEM Cloud Service环境中探索AI答案，验证性能和准确性，并在未来体验正式发布之前帮助塑造未来的体验。

若要请求参与或接收更新，请联系[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com)。

#### RDE快照(Beta计划) {#rde-snapshot-program}

在Beta版中，快速开发环境(RDE)现在支持一项功能，即拍摄代码和内容的当前状态的快照，之后可以恢复。 在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果您有兴趣使用此功能并提供反馈，请向[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)发送电子邮件。

#### 使用AI加速AEM开发(Alpha项目) {#ai-dev-alpha}

AEM Java栈栈团队越来越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI辅助开发，以加快功能交付并提高代码质量。 我们正在收集真实世界的体验，以帮助塑造未来Adobe支持的人工智能功能。

通过电子邮件发送[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)，共享您团队的工作成果，以及您希望Adobe提供的内容。

#### 扩展的应用程序性能监控 (APM)（Alpha 计划） {#apm-alpha}

在可观测性方面，AEM Cloud Service 目前支持 Adobe 提供的 [New Relic One](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) 和客户自管的 [Dynatrace](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。随着我们探索更多的 APM 选项，请将您偏好的厂商或技术以及用例发送至 [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com)。

## [!DNL Experience Manager] Guides {#guides}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表。

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
