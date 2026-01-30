---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service的最新发行说明'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 46a5a8f48a139ca1be13b400552569dc40fedcdd
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 38%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2026.1.0)的发布日期是2026年1月29日。 下一个功能版本(2026.2.0)计划于2026年2月26日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## AEM Beta程序 {#aem-beta-programs}

Adobe Experience Manager (AEM)测试版程序是客户访问预发行版功能和代码、提供反馈以及引导AEM未来的一种方式。

>[!IMPORTANT]
>
>Beta版本可能包含缺陷，并“按原样”提供，无任何类型的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持(通过Adobe支持服务或其他方式)Beta版。 Adobe建议客户谨慎使用，不要依赖测试版或随附的任何文档或材料的正确功能或性能。 Beta版中的功能和API如有更改，恕不另行通知。 因此，使用测试版完全由客户自行承担风险。

**参与的优点**
通过抢先使用Adobe正在开发的功能，客户和合作伙伴可以提供反馈并影响产品开发。 它还有助于客户在功能正式发布之前做好采用新功能的准备。

**当前测试版计划**
以下部分列出了活动的测试版计划。

### AEM(Beta程序)中的代理 {#agents-in-aem-beta-program}

提前获得对强大的新AEM代理功能的访问权限，这些功能涵盖生产、管理、优化、发现和开发。 您的反馈将直接影响Adobe的路线图和最终功能。 有关详细信息，请参阅[AEM代理概述](/help/ai-in-aem/agents/overview.md)。

该计划通常持续4-6周，但可以针对您的积极参与能力进行定制。

要选择加入此计划，请发送电子邮件至[aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com)，并尽可能包含以下详细信息：

* 将积极使用代理的团队成员的名称和Adobe ID。
* 列出您或您的团队将要使用的特定座席。 或者说“所有特工”

被选为参与的客户将由Adobe直接通知。 参与取决于资格考虑因素，包括客户许可和有限的计划能力。 虽然并非所有请求最初都可以得到满足，但可能会在未来测试阶段考虑添加其他客户。

### AEM Foundation(Beta项目) {#aem-foundation-beta-programs}

查看[AEM Foundation测试版计划](#foundation-early-adopter)。

### Cloud Manager(Beta项目) {#cloud-manager-beta-programs}

查看[Cloud Manager测试版计划](/help/implementing/cloud-manager/release-notes/current.md)。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Content MCP Server {#content-MCP}

AEM Cloud Service现在包括&#x200B;**内容MCP服务器**，为通过MCP兼容工具使用AEM内容的AI支持的体验提供了一种标准化方式。

使用聊天应用程序和代理平台的开发人员和高级用户可以将AEM连接到自定义协同功能和自动化，因此内容工作成为端到端业务工作流的一部分。

AEM提供两台服务器：

1. **只读内容MCP服务器** — 用于安全检索内容
1. **读/写内容MCP服务器** — 用于更改内容

这些MCP服务器包括用于处理&#x200B;**Pages**、**Content Fragments**&#x200B;和&#x200B;**Assets**&#x200B;的工具，并且可以从以下MCP客户端使用： **ChatGPT**、**Claude**、**Cursor**&#x200B;和&#x200B;**Microsoft Copilot Studio**。

在[将MCP与AEM云服务结合使用](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)中了解更多信息。 如有疑问或反馈，请发送电子邮件至[aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI 搜索**

AI 搜索引入了一种智能的上下文感知搜索体验，通过了解用户查询背后的含义和意图，该体验超越了传统关键词匹配。 它由AI和机器学习提供支持，即使查询用词不同、包含拼写错误、使用同义词或以不同语言提交，也能提供更准确的结果，帮助用户更快地找到相关内容，用更少的工作量。

有关详细信息，请参阅[Assets视图](/help/assets/search-assets-view.md#ai-search)和[管理员视图](/help/assets/search-assets.md#ai-search)中的AI 搜索。

**桌面应用程序3.0.1版**

[Desktop App 3.0.1（2025年12月20日）](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/release-notes)提高了关键工作流的可靠性、性能和稳定性。 此版本通过修复与AEM Author的同步问题来确保一致的文件夹命名，允许在活动传输期间不间断地使用应用程序，通过异步处理增强UI响应性，通过分页优化大型文件传输，并解决稳定性问题，包括在大型文件夹上传和下载期间创作服务器重新启动和崩溃的问题。

**Adobe Asset Link CEP 2026.01.0版本**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)在InDesign中引入了新的“重新链接缺少的链接”选项，该选项会自动从同一AEM文件夹重新链接其他缺少的资源。 该功能根据文件名匹配资源，显着减少了恢复断开链接时的手动工作。


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

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation重要声明 {#foundation-notices}

#### Java API弃用 {#java-api-deprecation}

不应再在代码中使用针对2026年2月26日删除的已弃用API。 要防止部署块，请在2026年3月26日之前删除API用法。 重要日期：

* **从2026年1月26日开始**：操作中心通知电子邮件将在每个环境&#x200B;**每周发送**&#x200B;以提醒删除这些API的使用情况。
* **2026年2月26日**：包含使用这些API的代码的Cloud Manager管道将在&#x200B;**代码质量**&#x200B;步骤期间&#x200B;**暂停**。 部署管理员、项目管理员或业务负责人可以覆盖此问题以允许管道继续。
* **2026年3月26日**：包含使用这些API的代码的Cloud Manager管道将在&#x200B;**代码质量**&#x200B;步骤期间&#x200B;**失败**，**阻止新代码的部署**，直到移除该使用为止。
* **2026年4月30日**：仍在使用这些API的环境可能&#x200B;**不再接收关键的Adobe版本更新**。

请查看[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整详细信息。但为了方便起见，下面列出了这些 API：

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

Adobe于2025年10月14日将&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;环境升级到更高性能的&#x200B;**Java 21运行时**。 从&#x200B;**2月9日**&#x200B;开始（逐步推出到2月11日），AEM Cloud Service SDK或任何云环境都不会使用Java 11运行时。

>[!NOTE]
>
> 要利用最新的性能优化和语言增强功能，建议使用Java 17或Java 21（首选）进行构建。 目前仍支持使用Java 8和Java 11进行构建，但将在即将发布的版本中弃用。 弃用之前，将单独发布通信。 请参阅&#x200B;*本文*&#x200B;的[生成时间要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)部分。
>

#### AEM Java 日志配置策略的执行 {#logconfig-policy}

AEM Java日志必须遵循标准格式，以确保在所有客户环境中进行可靠的监控。 自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

任何不受支持的自定义日志记录覆盖&#x200B;*现在将被忽略*。 大多数客户没有受到影响，Adobe已联系其当前配置可能受到影响的客户。

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

#### AEM Edge功能(Beta程序) {#edge-functions}

AEM Edge Functions(在之前的发行说明中称为&#x200B;*Edge Computing*)允许您在CDN层执行JavaScript，从而使数据处理更接近最终用户。 这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

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

#### 用于AEM Java和Dispatcher开发的IDE的AI工具(Beta程序) {#ai-dev-beta}

Java栈栈团队越来越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI辅助开发，以加快功能交付并提高代码质量。 加入Beta版以：

* 共享真实世界体验，以帮助塑造未来的Adobe支持的AI功能
* 尝试人工智能代理可用于生成和调试AEM代码和Dispatcher配置的IDE工具

电子邮件[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)以了解更多信息。

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
