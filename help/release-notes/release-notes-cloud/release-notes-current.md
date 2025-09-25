---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bdc0e7623592efed5270a3cb8322ef22e50cbad9
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 68%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.9.0)的发布日期是2025年9月25日。 下一个功能版本(2025.10.0)计划于2025年10月30日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440930?quality=12&captions=chi_hans)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites预发行版中的新增功能 {#prerelease-sites}

AEM内容片段的内容模型编辑器已经过现代化，与AEM中其他基于React光谱的界面保持一致。 其用户界面实施和可扩展性模型现在与内容片段编辑器和通用编辑器一致。 现在，从新的内容模型管理员UI打开新的模型编辑器时，默认使用新的模型编辑器。 在触屏UI中打开内容模型会打开触屏UI编辑器，并提供用于尝试新编辑器的功能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets视图中的新增功能 {#new-features-assets-view}

**Dynamic Media模板中带子字符串的增强文本格式**

您现在可以对Dynamic Media模板文本图层中的子字符串应用格式。 选定的单词或短语将被视为单独的图层，允许您调整其字体、字体大小、颜色等。 子字符串层已进行参数化，以便您可以使用模板的投放URL实时更新它

### 具有 OpenAPI 功能的动态媒体中的新功能 {#new-features-dynamic-media-with-openapi}

**带有 OpenAPI URL 的 SEO 友好型 DM**

使用 OpenAPI 创建用于在 DM 中交付资产的虚名 URL，用可读的短标识符替换系统生成的长 UUID。这使得关联变得 SEO 友好，并且与您的品牌或营销活动更加一致。虚名 URL 会在运行时自动解析为原始资产 UUID，不会中断现有工作流。

>[!NOTE]
>
>此功能作为“有限可用性”功能提供。 您可以[创建并提交 Adobe 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，为您的部署启用该功能。

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

**日期和时间输入组件**

现已提供[日期和时间组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)，用户可以使用日历和时钟界面选择日期和时间，也可以通过受支持的格式手动输入数值。

**改进了文件上传的错误处理**

[文件附件组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)现在会自动根据允许列表验证上传的文件类型。如果用户上传不受支持格式的文件，表单就会在提交过程中显示错误。该组件还检查文件内容以验证其类型，增强表单的整体安全性。

**指定了自定义提交操作的错误响应**

当[自定义提交操作](/help/forms/custom-submit-action-troubleshooting.md)遇到未处理的错误时，系统将返回错误代码 502。这有助于识别问题是否与自定义提交操作有关，使调试更容易。

**从记录文档中排除隐藏字段**

一个新属性允许从[记录文档](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)中排除隐藏字段。默认情况下此选项未选中，且适用于所有表单字段。


### AEM Forms 中的预发行版功能

**生成并同步 AFP 演绎版**

您现在可以使用 [AEM Forms Communication API](/help/forms/document-generation-afp-api.md) 将 XDP 文件转换为 AFP 格式。AFP 是一种广泛用于大型企业打印的高性能格式。

**规则编辑器的增强功能**

* [函数列表中的验证方法](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：现在支持在面板、字段和表单级别执行验证和重置方法。以前仅在表单级别支持这些方法。
* [现代 JavaScript 支持](/help/forms/rule-editor-core-components-difference-tables.md)：添加了自定义函数对 ECMAScript 2019 及更高版本功能的支持，让您可以编写更高效、模块化、可复用的代码。
* [规则编辑器中的下载 DoR 选项](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：规则编辑器中添加了一个下载记录文档 (DoR) 的功能，是一个开箱即用 (OOTB) 选项。

  ![记录文档](/help/forms/assets/document-of-record-rn.gif)

* [规则编辑器中的动态变量](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：您现在可以在规则编辑器中使用动态（临时）变量，以便更灵活地定义条件和操作。隐藏字段不再需要存储临时值。
* [支持基于自定义事件的规则](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：您现在可以定义自定义事件并根据这些事件触发规则。
* [上下文感知的可重复面板规则](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：在可重复面板中现在会根据上下文执行规则，而不是将规则仅应用于最后一个面板实例。
* [通过参数触发规则](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：规则编辑器现在支持基于查询参数、UTM 参数或浏览器参数执行规则。
* [表单特有的自定义函数](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)：Edge Delivery Services 表单现在支持表单特有的自定义函数脚本，这样可以更灵活地管理可复用逻辑。
* [自定义函数的静态导入](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：通用编辑器中的规则编辑器现在支持静态导入，允许开发人员在多个表单上组织、共享和复用函数。

### AEM Forms 中新的早期访问功能 {#forms-new-early-access-features}

AEM Forms 早期访问计划为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

这些发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

**潦草签名组件**

您现在可以使用[潦草签名组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)帮助用户在表单中添加签名，例如在合同表单中。该组件允许用户使用鼠标、触控笔或触摸屏直接在表单中绘制自己的签名。

**规则编辑器中的直接 API 集成**

自适应表单现在支持在可视化规则编辑器中[直接集成 API](/help/forms/api-integration-in-rule-editor.md)，无需表单数据模型。作者可以使用 URL 或 cURL 导入、映射输入/输出参数来配置 API，并通过身份验证确保安全调用。

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

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Release Management中的新增功能 {#new-features-release-management}

**暂停自动维护更新**

上线日、现场活动、销售高峰 — 这些时刻无法中断。 [我们新的自助服务功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)在需要的时候停止自动维护更新，以便您的团队集中精力。

* 安静时间：阻止在每天的设定时间进行自动维护。 适合工作时间、夜间跑步或早上切换。
* 无更新时段：阻止整周的自动维护。 将其用于启动项、促销活动或每年冻结。

>[!NOTE]
>
>9月25日作为有限可用功能提供。
>&#x200B;>请发送电子邮件至[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com)，以便在您的项目中激活它。

### 适用于Eclipse的AEM开发人员工具的新版本 {#aem-develeper-tools-for-eclipse}

已发布适用于Eclipse的AEM Developer Tools 1.4.0版本。 此版本添加了对Eclipse IDE 2022-12或更高版本的支持，并已通过当前版本(2025-09)的验证。 该工具现在可与AEM项目原型的现代版本配合使用，并包含了Sling IDE Tooling 1.3.0中的改进。

从[Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse)进行安装，有关更多详细信息，请参阅[AEM开发人员工具页面](https://eclipse.adobe.com)。

### 即将弃用 Java API {#java-api-deprecation}

多个已弃用的API在8月31日标记为删除，因此不应再引用。 如果在代码中检测到已弃用的API，您将会收到操作中心通知，11月13日之后，将在Cloud Manager构建期间显示通知，以强调删除使用的重要性。 请查看[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整详细信息。但为了方便起见，下面列出了这些 API：

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

已弃用&#x200B;*Java 11运行时*，并且大多数环境已升级到更高性能的&#x200B;**Java 21运行时**。

如果由于不支持的依赖项而无法升级环境（请参阅[Java 21运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您应该已经收到来自Adobe的电子邮件，其中包含后续步骤。 如该处所述，Adobe已于2025年9月18日&#x200B;**升级**&#x200B;开发&#x200B;**和** RDE **环境，以便您验证站点和流程并解决任何问题。**&#x200B;**阶段**&#x200B;和&#x200B;**生产**&#x200B;的升级将于&#x200B;**2025年10月14日**&#x200B;继续。

>[!NOTE]
>
>运行时版本与代码的构建版本不同。 虽然我们建议使用Java 21进行构建，但目前仍接受Java 11构建。 未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从&#x200B;**10月30日**&#x200B;开始，将忽略任何不受支持的自定义日志记录覆盖。 根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

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

### 适用于Edge Delivery Services的Edge身份验证(Beta计划) {#edge-authentication}

通过Edge身份验证，您可以将对Edge Delivery Services页面的访问限制为仅访问已通过您的身份提供程序(IdP)身份验证的用户。 这是通过部署OpenID Connect (OIDC)配置YAML文件实现的。

如有兴趣，请发送电子邮件至[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并提供用例的简短描述以及您可能遇到的任何问题。

请注意，我们今年早些时候发布了为AEM Cloud Service发布层项目[配置Open ID Connect ](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md)以保护AEM页面的功能(独立于Edge Delivery Services)。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### RDE 快照（Alpha 程序） {#rde-snapshot-program}

在 alpha 版本中，快速开发环境 (RDE) 现在支持对代码和内容的当前状态制作快照的功能，这些快照可以在以后恢复。在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果想提供关于此功能的反馈，请发送电子邮件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 日志转发至更多目标（Beta 项目） {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

现在在 beta 版本中，您可以将 AEM 日志转发到 Amazon S3、Sumo Logic、Dynatrace 以及您自己的 New Relic 帐户（不是 Adobe 提供的帐户）。请注意，这些日志记录目标支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

### 扩展的应用程序性能监控(APM) (Alpha计划) {#apm-alpha}

为了便于观察，AEM Cloud Service当前支持Adobe提供的[New Relic One](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic)和客户管理的[Dynatrace](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。 在我们探索对其他APM选项的支持时，请发送电子邮件至[aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com)，向您的首选供应商或技术发送电子邮件，并提供使用案例。


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
