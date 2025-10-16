---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 245ad07ba6abbf18e2011cb71a15948c9b92f80f
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 96%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本 (2025.9.0) 的发布日期为 2025 年 9 月 25 日。下一个功能版本 (2025.10.0) 计划于 2025 年 10 月 30 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440930?captions=chi_hans&quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 预发行中的新功能 {#prerelease-sites}

AEM 内容片段的内容模型编辑器已经过现代化，以与 AEM 中其他基于 React Spectrum 的界面保持一致。其用户界面实施和可扩展性模型现已与内容片段编辑器和通用编辑器保持一致。从新的内容模型管理员 UI 打开时，新的模型编辑器将作为默认选项。在触控 UI 中打开内容模型时，将会打开触控 UI 编辑器，并提供试用新编辑器的选项。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets 视图中的新功能 {#new-features-assets-view}

**Dynamic Media 模板中的子字符串文本增强格式化**

现在，您可以在 Dynamic Media 模板文本图层中对子字符串应用格式。选定的单词或短语将被视为单独的图层，可调整其字体、字号、颜色等属性。子字符串图层已参数化，因此您可以通过模板的投放 URL 实时更新。

### 具有 OpenAPI 功能的动态媒体中的新功能 {#new-features-dynamic-media-with-openapi}

**标记和可读的资源交付URL**

利用Dynamic Media中的OpenAPI虚URL，使带OpenAPI的Dynamic Media URL更易于用户读取。 虚URL允许将资产投放URL中系统生成的长且难以记忆的UUID替换为短的品牌控制标识符。 这使得虚URL更短、更易于阅读和共享，并允许更好地与您的品牌或营销活动保持一致。 虚名 URL 会在运行时自动解析为原始资产 UUID，不会中断现有工作流。

>[!NOTE]
>
>此功能作为“有限可用性”功能提供。您可以[创建并提交 Adobe 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，为您的部署启用该功能。

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

**针对 SharePoint 列表附件的调用表单数据模型工作流步骤**

调用表单数据模型的工作流步骤现在支持处理基于 SharePoint 列表的表单数据模型中 Base64 编码附件数组的工作流端元数据。通过此增强功能，工作流步骤可以传递、存储和检索每个附件的元数据，例如文件名、MIME 类型和自定义属性。这一功能实现了更全面的数据管理，并促进了下游的无缝集成。详情请参阅[针对 SharePoint 列表附件的调用表单数据模型工作流步骤增强支持](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step)。

### AEM Forms 中的预发行版功能

**规则编辑器增强功能**

规则编辑器现在支持增强的导航，并允许在输入参数中使用函数和数学表达式。

**支持事件负载的增强导航**

调用服务处理程序中的 `Navigate To` 操作现已支持 `EVENT_PAYLOAD`，使表单作者能够基于事件响应配置后续操作。此增强功能在设计提交后的工作流时提供了更大的灵活性，确保更顺畅的过渡和更个性化的用户体验。更多信息请参阅[支持事件负载的增强导航](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service)。

**输入参数中的函数与数学表达式支持**

输入参数现在支持函数调用和数学表达式，使表单作者能够直接传递动态计算的值。此增强功能简化了规则配置，消除了对额外字段的需求，使表单更适应复杂逻辑和计算驱动的场景。更多信息请参阅[输入参数中的函数与数学表达式支持](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters)。

### AEM Forms 中新的早期访问功能 {#forms-new-early-access-features}

AEM Forms 早期访问计划为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

这些发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

**交互式通信编辑器中的 PDF 预览**

用户可以在无数据、使用本地 JSON 数据文件或使用数据模型的数据情况下预览交互式通信 PDF，从而实现灵活的数据驱动测试。更多信息请参阅[交互式通信编辑器中的 PDF 预览](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md)。

**交互式通信中的自定义字体支持**

自定义字体功能允许用户在交互式通信中嵌入自定义或经组织批准的字体，确保在各类设备和平台上的 PDF 渲染保持一致并与品牌风格相符。更多信息请参阅[交互式通信中的自定义字体支持](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md)。

**交互式通信的导入与导出**

此功能支持在不同环境间迁移和复用交互式通信。您现在可以将交互式通信及其关联的片段和数据模型从一个环境导出，并导入到另一个环境。更多信息请参阅[交互式通信的导入与导出](/help/forms/interactive-communication/import-and-export-interactive-communications.md)。

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
>&#x200B;>请发送邮件至 [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) 以在您的项目中启用。

### 适用于 Eclipse 的 AEM 开发人员工具新版本 {#aem-develeper-tools-for-eclipse}

适用于 Eclipse 的 AEM 开发人员工具 1.4.0 已发布。该版本新增支持 Eclipse IDE 2022-12 或更高版本，并已在当前版本 (2025-09) 中通过验证。该工具现可与最新版本的 AEM 项目原型配合使用，并整合了 Sling IDE Tooling 1.3.0 的改进。

可通过 [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) 安装，并查看 [AEM 开发人员工具页面](https://eclipse.adobe.com)获取更多详情。

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

*Java 11 运行时*&#x200B;已弃用，大多数环境已升级至性能更高的 **Java 21 运行时**。

如果由于不受支持的依赖关系而无法升级环境（参见 [Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您应已收到来自 Adobe 的电子邮件，说明下一步操作。根据邮件说明，Adobe 已于 **2025 年 9 月 18 日**&#x200B;对您的&#x200B;**开发**&#x200B;和 **RDE** 环境进行升级，以便您验证网站和流程并解决相关问题。**暂存**&#x200B;和&#x200B;**生产**&#x200B;环境的升级将于 **2025 年 10 月 14 日**&#x200B;进行。

>[!NOTE]
>
>运行时版本与代码的构建版本是分开的。虽然我们建议使用 Java 21 进行构建，但目前仍接受基于 Java 11 的构建。未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

自 **10 月 30 日**&#x200B;起，任何不受支持的自定义日志覆盖都会被忽略。根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

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

### RDE 快照（Alpha 程序） {#rde-snapshot-program}

在 alpha 版本中，快速开发环境 (RDE) 现在支持对代码和内容的当前状态制作快照的功能，这些快照可以在以后恢复。在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果想提供关于此功能的反馈，请发送电子邮件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 日志转发至更多目标（Beta 项目） {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

现在在 beta 版本中，您可以将 AEM 日志转发到 Amazon S3、Sumo Logic、Dynatrace 以及您自己的 New Relic 帐户（不是 Adobe 提供的帐户）。请注意，这些日志记录目标支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

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
