---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service的最新发行说明'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9820b642af32960c532b238e00267cb4d880535f
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 28%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2026.3.0)的发布日期是2026年3月26日。 下一个功能版本(2026.4.0)计划于2026年4月30日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

&lt;##发布视频{#release-video}

请查看 2026 年 3 月发布概述视频，了解 2026.3.0 版本中的新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)

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

### 内容片段签出/签入 {#cf-checkout-in}

为了改进与AEM触屏UI的等同性，现在还可以使用新的内容片段管理UI签出和重新签入内容片段。 签出功能未更改，从而有效地锁定已签出的内容片段，从而防止其他用户在“内容片段编辑器”中编辑它。 拥有内容片段的用户和管理员可以签出片段并重新将其签入。 签出片段对引用的子片段或资产没有影响。

### 内容片段启动作业面板 {#cf-launches-jobs}

现在，可以在内容片段启动项管理UI的属性面板中查看内容片段启动项的异步作业以观察其状态 — 如果作业仍在运行、已完成或已中止，还可以查看有关作业的相关详细信息。

### 内容片段编辑器的RTE更新 {#cf-rte-update}

内容片段编辑器的富文本编辑器(RTE)已从TinyMCE迁移到TipTap。 这一变化带来了许多好处。

* 通用编辑器和内容片段编辑器现在使用相同的RTE技术栈栈。
   * 这意味着两个编辑器现在生成相同的HTML。
   * 扩展现在可以重用。
   * 现在，使用这两个编辑器（在Headless用例中）可获得相同的函数和方法。
   * 最终目标是一种配置可以在两个编辑器中带来统一的体验。
* 内容编辑器现在具有光谱2样式的新外观。
* 内容片段编辑器中提供了新功能，包括查找和替换以及成为内容顾问就绪。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

AEM Sites中的&#x200B;**内容顾问**

Content Advisor现在可在AEM Sites中使用，它直接从AEM Assets引入智能资源发现。 它使用户能够轻松地直接在其工作流中发现、浏览和重用最相关的资产，而无需切换上下文。

内容审查程序为资源提供了智能功能，例如基于活动简介的建议、上下文建议、对Dynamic Media演绎版的访问以及详细的资源元数据。

即将推出 — Content Advisor支持Adobe Workfront和AJO B2C应用程序，包括发现内容片段的功能

### Dynamic Media 中的新增功能 {#dynamic-media-new-features}

#### Dynamic Media模板编辑器更新 {#dynamic-media-template-editor-updates}

**层管理增强功能**

* 拖放图层重新排序：现在，可以通过拖动直接在“图层”面板中重新排序图层，从而提供一种比现有的“上移”或“下移”操作更快、更直观的方式来组织图层栈叠顺序。
* 复制、粘贴和复制：完全支持使用键盘快捷键(Cmd/Ctrl+C、V、D)或上下文菜单来复制、粘贴和复制图层，并支持多层选择。
* 单独的“图层属性”按钮：添加了专用的“图层属性”按钮，可更轻松地导航到图层设置，并且可通过双击支持图层来快速访问。

**文本格式功能**

* 行距控制：新的行距滑块允许精确控制文本图层中的行高，并具有完整的端到端支持，包括撤消/重做以及模板保存/加载。
* 全部大写格式：文本图层现在支持字体样式工具栏中的“全部大写格式”选项以及“粗体”、“斜体”和“下划线”。
* 垂直对齐选项：为文本图层添加了垂直对齐控件，以便在文本框中提供更精确的文本定位。

**大小和Dimension控件**

* 宽高比解锁：用户现在可以在调整大小属性时解锁宽高比，从而可独立调整宽度和高度，以实现更灵活的图层大小调整。
* 组排文字行配置：在文本组排文字属性中添加了对`copyfitlines`和`copyfitmaxlines`设置的支持，从而对文本组排行为提供了更精细的控制。

**视觉波兰语**

* 更新了“计时器”和“形状”层的图标，并细化了“频谱2(S2)”设计系统图标。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的早期访问功能 {#forms-early-access-features}

**在提交PDF中显示多选下拉列表的标签**
自适应Forms中的多选下拉组件现在在[生成的提交PDF](/help/forms/generate-document-of-record-core-components.md)中呈现其选定的显示标签，以确保文档准确反映用户在表单上看到的内容。

**复选框、单选按钮和面板组件的增强辅助功能**
自适应Forms核心组件为[复选框组(v2)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[单选按钮组(v2)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button)和[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)引入了符合WCAG 2.2的语义标记。 这些组件利用`<fieldset>`和`<legend>`个HTML元素在组标签及其选项之间建立有意义的关系，从而使屏幕阅读器和其他辅助技术能够进行准确解释。

Forms Manager中的&#x200B;**版本控制支持**
Forms Manager现在[支持自适应Forms（核心组件和基础组件）](/help/forms/manage-form-versions-forms-manager.md)、表单片段、主题、XDP模板和二进制资源的版本控制。 直接从Forms和文档控制台创建版本、查看完整的版本历史记录以及恢复表单资产的早期状态。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础 {#foundation}

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation的新功能 {#foundation-new}

#### 简化的索引管理 {#simplified-index-management}

[简化的索引管理](https://oak-indexing.github.io/oakTools/simplified.html)提供了一种更简单的方法，用于定义自定义索引和使用一个JSON文件自定义开箱即用(OOTB)索引，而无需复制完整定义或手动管理版本。 自定义项会与最新的OOTB索引合并，并在需要时创建新索引版本。

#### Cloud Manager MCP服务器 {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

现代IDE使用模型上下文协议(Model Context Protocol， MCP)来启用大型语言模型(Large Language Model， LLM)以调用MCP服务器公开的工具。 开发人员可以简单地用自然语言描述他们的意图，而不是直接与低级API规范集成。

Cloud Manager MCP服务器允许您通过提示直接从IDE与Cloud Manager API交互。 支持的方案包括执行管道、检查环境状态等。

了解有关[AEM MCP服务器](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)的更多信息。

### [!DNL Experience Manager]作为[!DNL Cloud Service] Foundation重要声明 {#foundation-notices}

#### Java API弃用 {#java-api-deprecation}

不应再在代码中使用针对2026年2月26日删除的已弃用API。 要阻止部署块，请在&#x200B;**2026年3月30日**&#x200B;之前删除API用法。 重要日期：

* **从2026年1月26日开始**：操作中心通知电子邮件将作为提醒发送，以删除这些API的使用情况。
* **2026年2月26日**：包含使用这些API的代码的Cloud Manager管道将在&#x200B;**代码质量**&#x200B;步骤期间&#x200B;**暂停**。 部署管理员、项目管理员或业务负责人可以覆盖此问题以允许管道继续。 *这可能会降低验证和发布代码更改的能力。*
* **2026年3月30日**：包含使用这些API的代码的Cloud Manager管道将在&#x200B;**代码质量**&#x200B;步骤期间&#x200B;**失败**。 在删除已弃用的API用法之前，将阻止部署。 *这可能会阻止您发布时效性更新，并可能影响您的业务运营。*
* **2026年5月4日**：仍在使用已弃用API的环境&#x200B;**将不会收到关键的Adobe版本更新**，并且不受Adobe有关性能和可用性的标准承诺的约束。 因此，您将不会收到新功能或错误修复，应用程序的稳定性和正常运行时间可能会受到负面影响，并且安全风险暴露可能会进一步增加。

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

#### 用于AEM Java和Dispatcher开发的IDE AI工具（公共Beta程序） {#ai-dev-beta}

Java栈栈团队越来越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI辅助开发，以加快功能交付并提高代码质量。

参与公共测试版（无需注册）以尝试编码代理可用于生成和调试AEM代码和Dispatcher配置的IDE工具。

在[使用AI工具进行本地开发](/help/ai-in-aem/local-development-with-ai-tools.md)测试版文档和电子邮件[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)中了解更多信息（如有疑问或反馈）。

#### AEM Edge功能（Beta程序） {#edge-functions}

AEM Edge Functions允许您在CDN层执行JavaScript，使数据处理更接近于最终用户。 这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，重新设置响应的格式
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

#### 使用开发代理进行Web层配置管道故障排除（Beta程序） {#devagent-webtier}

开发代理的[管道疑难解答](/help/ai-in-aem/agents/brand-experience/development/development.md)功能可帮助开发人员高效地诊断和解决AEM as a Cloud Service部署中的问题。 除了支持全栈管道（部署和代码质量）之外，开发代理现在还支持将&#x200B;**Web层配置管道**&#x200B;的故障排除作为Beta程序的一部分。

若要请求访问测试版，请发送电子邮件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。 需要预先具备对AEM中代理的访问权限。

#### 适用于AEM 6.5到AEM Cloud Service迁移的IDE AI工具（Alpha程序） {#cm-ide-migration}

使用IDE AI工具根据[最佳实践分析器报告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)的建议执行操作，加快从AEM 6.5到AEM as a Cloud Service （Java栈栈）的迁移。

电子邮件[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)以了解更多信息。

#### Edge Delivery Services 的边缘身份验证（Beta 计划） {#edge-authentication}

边缘身份验证可让您将对 Edge Delivery Services 页面的访问限制为仅限已通过身份标识提供者 (IdP) 认证的用户。此功能通过部署 OpenID Connect (OIDC) 配置 YAML 文件来实现。

如有兴趣，请发送邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并简要说明您的用例及相关问题。

#### 金丝雀生产部署：在接受真实流量前测试代码（Beta 计划） {#canary-beta}

您可以在对最终用户开放前，先使用仅限内部的测试流量验证生产构建。将构建部署到生产环境，仅通过特殊标头路由金丝雀流量，监控行为，然后再决定是否提升为真实流量或回滚——而不会影响客户。

您可以将代码发布部署到生产环境，但在决定接受真实流量或回滚之前，仅将其限制在内部测试流量中。

如需申请访问权限并分享反馈，请发送邮件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com)。

#### RDE快照（Beta计划） {#rde-snapshot-program}

在Beta版中，快速开发环境(RDE)现在支持一项功能，即拍摄代码和内容的当前状态的快照，之后可以恢复。 在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果您有兴趣使用此功能并提供反馈，请向[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)发送电子邮件。

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
