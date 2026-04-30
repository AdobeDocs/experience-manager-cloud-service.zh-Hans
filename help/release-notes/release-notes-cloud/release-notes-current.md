---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service的最新发行说明'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d389f158ddd71f90b5ee9b707050f5b593ec595a
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 31%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2026.4.0)的发布日期是2026年4月30日。 下一个功能版本(2026.5.0)计划于2026年5月28日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483070/?captions=chi_hans&quality=12)
-->

## AEM Beta程序 {#aem-beta-programs}

Adobe Experience Manager (AEM)测试版程序是客户访问预发行版功能和代码、提供反馈以及引导AEM未来的一种方式。

>[!IMPORTANT]
>
>Beta版本可能包含缺陷，并“按原样”提供，无任何类型的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持（通过Adobe支持服务或其他方式）Beta版。 Adobe建议客户谨慎使用，不要依赖测试版或随附的任何文档或材料的正确功能或性能。 Beta版中的功能和API如有更改，恕不另行通知。 因此，使用测试版完全由客户自行承担风险。

**参与的优点**

通过抢先使用Adobe正在开发的功能，客户和合作伙伴可以提供反馈并影响产品开发。 它还有助于客户在功能正式发布之前做好采用新功能的准备。

**当前测试版计划**

以下部分列出了活动的测试版计划。

### AEM中的代理 {#agents-in-aem}

如果您想在生产、管理、优化、发现和开发中探索强大而新的AEM代理功能，[请在此处了解如何访问它们。](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation（Beta项目） {#aem-foundation-beta-programs}

查看[AEM Foundation测试版计划](#foundation-early-adopter)。

### Cloud Manager（Beta项目） {#cloud-manager-beta-programs}

查看[Cloud Manager测试版计划](/help/implementing/cloud-manager/release-notes/current.md)。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 人工智能翻译集成 {#ai-translation-integration}

AEM用户现在可以利用大型语言模型(LLM)进行内容翻译，以机器翻译的速度提供人工翻译质量。 与传统第三方翻译服务类似，Azure OpenAI可在AEM中配置为翻译提供商，并支持计划在未来版本中使用的其他LLM。 客户使用自己的LLM许可证来实现此功能。 此外，可以将公司翻译风格指南上传到AEM，从而提取翻译规则以确保品牌和风格的一致性。 有关详细信息，请参阅[配置AI翻译集成](/help/sites-cloud/administering/translation/ai-translation-integration.md)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**内容顾问现在可用于Adobe Workfront和非Adobe应用程序**

Content Advisor现在可用于Adobe Workfront和非Adobe（第三方）应用程序，从而将智能资源发现和内容重用扩展到Adobe Express和AEM Sites之外。 此版本提供了全面的内容顾问体验，包括AI支持的搜索、上下文感知推荐、基于活动简报的发现、对Dynamic Media演绎版的访问、内容片段发现、过滤器和资源元数据到Adobe Workfront工作流和外部应用程序。

您现在可以直接在首选应用程序中发现、评估和重复使用AEM Assets中已批准的资源，从而在Adobe和非Adobe应用程序中实现一致的资源使用、提高效率和简化内容创建。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的早期访问功能 {#forms-early-access-features}

**在提交PDF中显示多选下拉列表的标签**
自适应Forms中的多选下拉组件现在在[生成的提交PDF](/help/forms/generate-document-of-record-core-components.md)中呈现其选定的显示标签，确保文档准确反映用户在表单上看到的内容。

**复选框、单选按钮和面板组件的增强辅助功能**
自适应Forms核心组件为[复选框组(v2)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[单选按钮组(v2)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button)和[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)引入了符合WCAG 2.2的语义标记。 这些组件利用`<fieldset>`和`<legend>`个HTML元素在组标签及其选项之间建立有意义的关系，从而使屏幕阅读器和其他辅助技术能够进行准确解释。

Forms Manager中的&#x200B;**版本控制支持**
Forms Manager现在[支持自适应Forms（核心组件和基础组件）](/help/forms/manage-form-versions-forms-manager.md)、表单片段、主题、XDP模板和二进制资源的版本控制。 直接从Forms和文档控制台创建版本、查看完整的版本历史记录以及恢复表单资产的早期状态。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础 {#foundation}

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation的新功能 {#foundation-new}

#### 用于AEM Java和Dispatcher开发的IDE人工智能工具 {#ai-dev}

Java栈栈团队越来越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI辅助开发，以加快功能交付并提高代码质量。

编码代理可以使用IDE工具来生成和调试AEM代码和Dispatcher配置。 例如，下面的视频演练演示了使用“代理技能”构建AEM组件。

了解有关[使用AI工具进行本地开发](/help/ai-in-aem/local-development-with-ai-tools.md)的更多信息，并随时发送电子邮件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)，提出问题或反馈。


>[!VIDEO](https://video.tv.adobe.com/v/3484988/?captions=chi_hans&learn=on&enablevpops)

#### Experience Governance MCP服务器 {#gov-mcp-server}

Experience Governance MCP Server现已正式提供(GA)。 它与支持模型上下文协议(MCP)的AI开发人员工具和聊天机器人集成，允许您在聊天机器人或IDE中使用自然语言提示来维护品牌完整性和合规性。 您可以根据品牌治理规则评估内容（文本、图像、页面），并检索品牌配置和可用的治理检查。

了解有关[AEM MCP服务器](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)和[治理代理](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview)的更多信息。

#### 克劳德连接器 {#aem-claude-connector}

Claude用户可以浏览Anthropic的[连接器市场](https://claude.ai/settings/connectors)以一键安装[Adobe Experience Manager连接器](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector)。 此MCP服务器公开一组用于与AEM进行交互的工具，包括通过提示编辑内容。

#### 关于发布新功能的AEM OIDC {#aem-oidc-on-publish-new-features}

* 修复：验证后，原始请求中的查询参数丢失
* OIDC身份验证[文档](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication)中的身份验证后的自定义重定向

#### Microsoft Graph API的邮件服务支持 {#mail-service-graph-api}

AEM的邮件服务现在支持使用Microsoft Graph API的Microsoft® Outlook（通过Microsoft 365）。 这对于不允许SMTP（邮件服务已支持此功能）的组织特别有用。 身份验证通过OAuth 2.0进行。 [了解如何配置](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api)。

#### CDN日志可以转发到Sumo Logic {#sumo-cdn-logforwarding}

[日志转发功能](/help/implementing/developing/introduction/log-forwarding.md#sumologic)现在支持将CDN日志发送到Sumo Logic。 以前，日志转发到Sumo Logic的功能仅限于AEM日志。

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation重要声明 {#foundation-notices}

#### IMS身份验证富错误 {#ims-auth-rich-errors}

为帮助解决IMS集成问题，`imsauth`已添加对&#x200B;*富错误*&#x200B;的支持。

这些错误不只返回HTTP状态代码，而是提供了额外的上下文来帮助诊断和解决可能会阻止身份验证和访问的问题。

#### Java API弃用 {#java-api-deprecation}

删除使用已弃用的API至关重要。

自&#x200B;**4月14日**&#x200B;起，包含使用针对2026年2月26日删除&#x200B;**的API的代码的Cloud Manager管道在代码质量**&#x200B;步骤中失败。 在删除已弃用的API用法之前，将阻止部署。 *这可能会阻止您发布时效性更新，并可能影响您的业务运营。*

从&#x200B;**2026年6月11日开始**，仍在使用这些已弃用API **的环境将不会收到关键Adobe版本更新**，并且不会受Adobe有关性能和可用性的标准承诺的约束。 因此，您将不会收到新功能或错误修复，应用程序的稳定性和正常运行时间可能会受到负面影响，并且安全风险敞口可能会进一步增加。

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
* `org.apache.jackrabbit.oak.plugins.memory`

+++

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation早期采用者功能 {#foundation-early-adopter}

#### AEM Edge功能（Beta程序） {#edge-functions}

[AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md)允许您在CDN层执行JavaScript，使数据处理更接近于最终用户。 这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，重新设置响应的格式
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为ChatGPT和Claude等AI助理公开MCP服务器以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。 如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

#### Web层配置管道故障排除（Beta程序） {#devagent-webtier}

开发代理的[管道疑难解答](/help/ai-in-aem/agents/brand-experience/development/development.md)功能可帮助开发人员高效地诊断和解决AEM as a Cloud Service部署中的问题。 除了支持全栈管道（部署和代码质量）之外，开发代理现在还支持将&#x200B;**Web层配置管道**&#x200B;的故障排除作为Beta程序的一部分。

若要请求访问测试版，请发送电子邮件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。 需要预先具备对AEM中代理的访问权限。

#### 复制AI故障排除（Alpha项目） {#replication-ai-troubleshooting-alpha}

在AEM创作和其他界面中使用AI助手，可以对与复制相关的问题（如阻止的队列）进行故障诊断。 要加入Alpha计划，请发送电子邮件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)，说明您的兴趣。

#### 适用于AEM 6.5到AEM Cloud Service迁移的IDE AI工具（Beta程序） {#cm-ide-migration}

使用IDE AI工具根据[最佳实践分析器报告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)的建议执行操作，加快从AEM 6.5到AEM as a Cloud Service （Java栈栈）的迁移。

请发送电子邮件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)，以了解更多信息并请求访问功能。

#### Edge Delivery Services 的边缘身份验证（Beta 计划） {#edge-authentication}

边缘身份验证可让您将对 Edge Delivery Services 页面的访问限制为仅限已通过身份标识提供者 (IdP) 认证的用户。 此功能通过部署 OpenID Connect (OIDC) 配置 YAML 文件来实现。

如有兴趣，请发送邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并简要说明您的用例及相关问题。

#### 金丝雀生产部署：在接受真实流量前测试代码（Beta 计划） {#canary-beta}

您可以在对最终用户开放前，先使用仅限内部的测试流量验证生产构建。 将构建部署到生产环境，仅通过特殊标头路由金丝雀流量，监控行为，然后再决定是否提升为真实流量或回滚——而不会影响客户。

如需申请访问权限并分享反馈，请发送邮件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com)。

#### RDE快照（Beta计划） {#rde-snapshot-program}

在Beta版中，快速开发环境(RDE)现在支持功能[拍摄代码和内容的当前状态的快照](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots)，以便稍后恢复。 在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。 还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果您有兴趣使用此功能并提供反馈，请向[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)发送电子邮件。

#### 扩展的应用程序性能监控 (APM)（Alpha 计划） {#apm-alpha}

在可观测性方面，AEM Cloud Service 目前支持 Adobe 提供的 [New Relic One](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) 和客户自管的 [Dynatrace](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。 随着我们探索更多的 APM 选项，请将您偏好的厂商或技术以及用例发送至 [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com)。

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
