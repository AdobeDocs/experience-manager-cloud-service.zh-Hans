---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.8.0 版的发行说明。'
feature: Release Information
role: Admin
source-git-commit: 4187f9bb08d8af214054b937a5426e95c1de748d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.8.0 版的发行说明 {#release-notes}

以下部分概述了 2025.8.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.8.0) 的发布日期为 2025 年 8 月 28 日。下一个功能版本 (2025.9.0) 计划于 2025 年 9 月 25 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) 是您访问所有 AEM 功能的统一起点。它根据您的用户角色和可用的许可证进行个性化，使每个用户都能高效实现自己的目标。

## AEM 中的 AI 助手 {#AI-assistant}

AEM 的 [AI 助手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)提供了一个对话界面，旨在让您立即获得 AEM 产品相关问题的回答（*为所有用户提供*），并能自动创建支持票证（*为支持管理员提供*）。它直接嵌入在 AEM 中，可从 AEM Experience Hub、Cloud Manager 和 Author UI 访问。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#enhancements-sites}

* 在内容片段管理用户界面中，您现在可以查看内容片段的工作流状态，其中包含关于所选片段的过去和当前正在运行的工作流的详细信息。
* 在新的内容片段编辑器中，通过 UUID 而不是通过路径打开内容片段，使性能在常见情况下提高了 25%。
* 当复制带引用片段的内容片段时，引用片段的副本现在存储在与父级片段副本相同的位置。
* 您现在可以在文件夹设置中配置一个自定义工作区，以将内容片段导出到 Adobe Target 中配置的工作区。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Content Hub 的新功能 {#new-features-content-hub}

**通过过滤器属性进行批量搜索**

Content Hub 现在可以更快地发现您需要的资产。使用新的批量搜索功能，您可以为任何过滤器属性以分隔符分隔的方式输入多个值（例如多个 SKU ID），只通过一个搜索就能立即检索所有匹配的资产。

### 具有 OpenAPI 功能的动态媒体中的新功能 {#new-features-dynamic-media-with-openapi}

**带有 OpenAPI URL 的 SEO 友好型 DM**

使用 OpenAPI 创建用于在 DM 中交付资产的虚名 URL，用可读的短标识符替换系统生成的长 UUID。这使得关联变得 SEO 友好，并且与您的品牌或营销活动更加一致。虚名 URL 会在运行时自动解析为原始资产 UUID，不会中断现有工作流。

>[!NOTE]
>
>此功能将于 9 月 10 日作为有限发布版推出。您可以[创建并提交 Adobe 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，为您的部署启用该功能。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [日期和时间输入组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)：现在提供一个日期和时间组件，用户可以使用日程表和时钟界面选择日期和时间，也可以支持的格式手动输入数值。
* [改进了文件上传错误处理](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)：文件附件组件现在会自动根据允许列表验证上传的文件类型。如果用户上传不受支持格式的文件，表单就会在提交过程中显示错误。该组件还检查文件内容以验证其类型，增强表单的整体安全性。
* [自定义提交操作的特定错误响应](/help/forms/custom-submit-action-troubleshooting.md)：当自定义提交操作遇到未经处理的错误时，就会返回错误代码 502。这有助于识别问题是否与自定义提交操作有关，使调试更容易。
* [从记录文档中排除隐藏字段](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)：添加了一个新属性，允许从记录文档中排除隐藏字段。默认情况下此选项未选中，且适用于所有表单字段。

### AEM Forms 中的预发行版功能

* [生成并同步 AFP 演绎版](/help/forms/document-generation-afp-api.md)：您现在可以使用 AEM Forms Communication API 将 XDP 文件转换为 AFP 格式。AFP 是一种广泛用于大型企业打印的高性能格式。
* **规则编辑器的增强功能**
   * [函数列表中的验证方法](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：现在支持在面板、字段和表单级别执行验证和重置方法。以前仅在表单级别支持这些方法。
   * [现代 JavaScript 支持](/help/forms/rule-editor-core-components-difference-tables.md)：添加了自定义函数对 ECMAScript 2019 及更高版本功能的支持，让您可以编写更高效、模块化、可复用的代码
   * [规则编辑器中的下载 DoR 选项](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：规则编辑器中添加了一个下载记录文档 (DoR) 的功能，是一个开箱即用 (OOTB) 选项。
     ![记录文档](/help/forms/assets/document-of-record-rn.gif)
   * [规则编辑器中的动态变量](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：您现在可以在规则编辑器中使用动态（临时）变量，以便更灵活地定义条件和操作。隐藏字段不再需要存储临时值。
   * [支持基于自定义事件的规则](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：您现在可以定义自定义事件并根据这些事件触发规则。
   * [上下文感知的可重复面板规则](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：在可重复面板中现在会根据上下文执行规则，而不是将规则仅应用于最后一个面板实例。
   * [通过参数触发规则](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：规则编辑器现在支持基于查询参数、UTM 参数或浏览器参数执行规则。
   * [表单特有的自定义函数](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)：Edge Delivery Services 表单现在支持表单特有的自定义函数脚本，这样可以更灵活地管理可复用逻辑。
   * [自定义函数的静态导入](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：通用编辑器中的规则编辑器现在支持静态导入，允许开发人员在多个表单上组织、共享和复用函数。

### AEM Forms 中的早期采用者功能

* [潦草签名组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)：您现在可以使用潦草签名组件帮助用户在表单中添加签名，例如合同表单。该组件允许用户使用鼠标、触控笔或触摸屏直接在表单中绘制自己的签名。
* [规则编辑器中的直接 API 集成](/help/forms/api-integration-in-rule-editor.md)：自适应表单现在支持在可视化规则编辑器中直接集成 API，无需表单数据模型。作者可以使用 URL 或 cURL 导入、映射输入/输出参数来配置 API，并通过身份验证确保安全调用。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### JavaScript 编译更新 {#javascript-compilation}

现在，默认的客户端库（clientlibs）JavaScript 编译输出目标是 ECMASCRIPT_2018 而不是 ECMASCRIPT5。虽然过去可以覆盖配置，但这一更新默认启用了增强的性能和现代 JavaScript 语法及功能。

### 即将弃用 Java API {#java-api-deprecation}

一些已弃用的 API 将于 8 月 31 日被移除，因此不应再引用。9 月初，在检测到使用 API 时会发送操作中心通知。9 月 25 日之后，会在 Cloud Manager 构建过程中显示通知，强调移除 API 使用的重要性。请查看[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整详细信息。但为了方便起见，下面列出了这些 API：

<details>
  <summary>展开查看 Java API 弃用项</summary>

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
</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Java 11 运行时弃用 {#java11-runtime-deprecation}

*Java 11 运行时环境*&#x200B;现已弃用，大多数环境已经升级到性能更高的 **Java 21 运行时环境**。

如果由于存在不受支持的依赖项（请参阅 [Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您的环境无法升级，您应该已经收到了 Adobe 发来的电子邮件，其中包含了具体的后续操作步骤。请确保在 **2025 年 10 月 1 日**&#x200B;之前完成所有必要的更新，以确保您的环境能够在不中断的情况下进行升级。

注意：运行时版本与代码的构建版本是分开的。虽然我们建议使用 Java 21 进行构建，但目前仍支持使用 Java 11 进行构建。未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从 **9 月 25 日**&#x200B;开始，任何不受支持的自定义日志记录覆盖都将被忽略。根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### 边缘计算（Beta 计划） {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 在授予内容访问权限之前，通过身份标识提供商对用户进行身份验证
* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，重新设置响应的格式
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的 CDN 配置（Beta 计划） {#cdn-eds-beta}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在在 beta 版中，您可以为内容传递网络源选择器、响应和请求转换、内容传递网络日志转发等功能部署一个配置管道。请联系 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 并提供您的用例详情。

### RDE 快照（Alpha 程序） {#rde-snapshot-program}

在 alpha 版本中，快速开发环境 (RDE) 现在支持对代码和内容的当前状态制作快照的功能，这些快照可以在以后恢复。在将可能需要恢复的代码同步时，或在不同功能的开发之间切换时，这个功能很有用。还可以仅恢复可变内容，将其作为一个已知的测试起点。

如果想提供关于此功能的反馈，请发送电子邮件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 日志转发至更多目标（Beta 项目） {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

现在在 beta 版本中，您可以将 AEM 日志转发到 Amazon S3、Sumo Logic、Dynatrace 以及您自己的 New Relic 帐户（不是 Adobe 提供的帐户）。请注意，这些日志记录目标支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

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
