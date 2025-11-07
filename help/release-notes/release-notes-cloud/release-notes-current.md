---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a5e20bd3ee4d332b46bdff2fbf5222c9a9fead2f
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 59%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.10.0)的发布日期是2025年10月30日。 下一个功能版本(2025.11.0)计划于2025年11月20日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440930?captions=chi_hans&quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#new-sites}

* [内容片段的启动项](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)：内容作者现在可以使用内容片段的启动项创建和计划结构化内容的未来变体。 新的内容片段控制台允许创建、编辑、管理和计划内容片段启动作为可与源分支同步的将来内容的分支。 新的差异视图在提交Launch以供未来发布之前提供了所有内容更改的清晰概述。

* AEM内容片段[的](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)内容模型编辑器已进行现代化改造，以便与AEM中其他基于React光谱的界面保持一致。 其用户界面实施和可扩展性模型现已与内容片段编辑器和通用编辑器保持一致。从新的内容模型管理员 UI 打开时，新的模型编辑器将作为默认选项。在触控 UI 中打开内容模型时，将会打开触控 UI 编辑器，并提供试用新编辑器的选项。

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms 的新增功能 {#new-features-forms}

**用于自适应表单和表单片段的通用编辑器**

通用编辑器现在为创建自适应Forms和可重用的表单片段提供统一的创作体验。 利用强大的扩展和全面的提交功能，创作者可以在直观的WYSIWYG环境中以可视方式设计表单。 该编辑器集成了reCAPTCHA验证功能以增强安全性，提供了预填充服务以减少手动输入，并支持所有设备的响应式设计。

**可用扩展：**

* **规则编辑器**：可视化规则编辑器允许表单作者向表单字段添加动态行为，而无需编码、支持事件驱动规则、即时验证和错误处理。
* **表单属性**：一个向导，可帮助用户直接在编辑器中配置提交操作、预填充服务、感谢消息以及其他与表单相关的行为。
* **表单数据Source和绑定引用**：数据源扩展允许表单作者将与数据模型关联的组件直接添加到自适应表单中，并从所有组件的树选择中选择绑定引用。

**支持的提交操作：**

通用编辑器支持广泛的提交工作流，包括自定义提交操作、提交到Microsoft SharePoint、提交到Microsoft OneDrive、提交到Azure Blob Storage、提交到REST端点、调用AEM工作流、调用Power Automate流、提交到Marketo Engage、提交到Adobe Experience Platform (AEP)、提交到电子表格、使用表单数据模型(FDM)提交、提交到Workfront Fusion和发送电子邮件。

有关完整的详细信息，请参阅Forms的[Edge Delivery Services通用编辑器文档](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)。 有关配置提交操作的信息，请参阅[自适应表单提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

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

### 版本管理中的新功能 {#new-features-release-management}

**暂停自动维护更新**

上线日、直播活动、销售高峰——这些关键时刻绝不能出问题。[我们的新自助功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)可在关键时段阻止自动维护更新，确保您的团队专注无扰。

* 安静时段：在每天设定的时间内阻止自动维护更新。非常适合工作时段、夜间任务或早间切换。
* 无更新周期：阻止长达一周的自动维护更新。可用于产品发布、促销活动或年度冻结。

>[!NOTE]
>
>此功能自 9 月 25 日起作为有限可用性功能提供。
>请发送邮件至 [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) 以在您的项目中启用。

### AEM日志转发到更多目标 {#log-forwarding}

现在，可以将AEM日志转发到Amazon S3、Sumo Logic、Dynatrace以及您自己的New Relic帐户(而不是Adobe提供的帐户)。 请注意，这些日志记录目标支持AEM日志(包括Apache/Dispatcher)，但CDN日志不支持。

查看[支持的日志转发目标](/help/implementing/developing/introduction/log-forwarding.md)的完整集合。

### Edge Delivery Services的配置管道 {#config-pipeline-eds}

现在，使用Edge Delivery Services构建的站点支持配置管道，从而扩展此功能而不只是AEM创作和AEM发布交付。 您可以使用配置管道管理CDN配置等设置，包括流量过滤器规则和源选择器。 请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

Edge Delivery 配置管道同样支持通过 Cloud Manager 管道变量管理密钥。

请参阅[添加 Edge Delivery 管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。

### 即将弃用 Java API {#java-api-deprecation}

若干已弃用的 API 于 8 月 31 日被标记为移除，因此不应再被引用。如果在您的代码中检测到使用了弃用 API，您将会在操作中心收到通知。自 11 月 13 日起，在 Cloud Manager 构建过程中也会显示提示，以进一步强调移除弃用 API 的重要性。请查看[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整详细信息。但为了方便起见，下面列出了这些 API：

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

### Java 11 运行时弃用 {#java11-runtime-deprecation}

Adobe于2025年10月14日将&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;环境升级到更高性能的&#x200B;**Java 21运行时**。 从1月下旬开始，AEM Cloud Service SDK和任何云环境都不会使用Java 11运行时。

>[!NOTE]
>
> 要利用最新的性能优化和语言增强功能，建议使用Java 17或Java 21（首选）进行构建。 目前仍支持使用Java 8和Java 11进行构建，但将在即将发布的版本中弃用。 弃用之前，将单独发布通信。 请参阅&#x200B;*本文*&#x200B;的[生成时间要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)部分。
>

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从&#x200B;**11月20日**&#x200B;开始，将忽略任何不受支持的自定义日志记录覆盖。 根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### 边缘计算（Beta 计划） {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，重新设置响应的格式
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的边缘身份验证（Beta 计划） {#edge-authentication}

边缘身份验证可让您将对 Edge Delivery Services 页面的访问限制为仅限已通过身份标识提供者 (IdP) 认证的用户。此功能通过部署 OpenID Connect (OIDC) 配置 YAML 文件来实现。

如有兴趣，请发送邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并简要说明您的用例及相关问题。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### 金丝雀生产部署：在接受真实流量前测试代码（Beta 计划） {#canary-beta}

您可以在对最终用户开放前，先使用仅限内部的测试流量验证生产构建。将构建部署到生产环境，仅通过特殊标头路由金丝雀流量，监控行为，然后再决定是否提升为真实流量或回滚——而不会影响客户。

您可以将代码发布部署到生产环境，但在决定接受真实流量或回滚之前，仅将其限制在内部测试流量中。

如需申请访问权限并分享反馈，请发送邮件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com)。


### 人工智能答案 — 适用于AEM Sites (Beta程序)的更智能、上下文感知响应 {#ai-answers-beta}

人工智能解答为访客引入了一种与内容交互的新方法。 它通过检索 — 增强型生成(RAG)技术提供支持，利用您的AEM管理的数据直接在您的数字体验中提供准确、品牌一致的答案。

作为此测试版的一部分，您可以在AEM Cloud Service环境中安全地探索AI答案。 通过这种方法，您可以在向实时受众发布之前验证性能、准确性和整体体验。 验证后，您可以将AI答案体验提升到完全生产环境。

若要请求访问测试版或分享您的反馈，请联系[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com)。


### RDE 快照（Alpha 程序） {#rde-snapshot-program}

在 alpha 版本中，快速开发环境 (RDE) 现在支持对代码和内容的当前状态制作快照的功能，这些快照可以在以后恢复。在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果想提供关于此功能的反馈，请发送电子邮件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### 扩展的应用程序性能监控 (APM)（Alpha 计划） {#apm-alpha}

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
