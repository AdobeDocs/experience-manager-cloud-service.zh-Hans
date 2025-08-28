---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 96022123209fff18548b77a4cbd63ccec697119b
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 46%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.8.0)的发布日期是2025年8月28日。 下一个功能版本(2025.9.0)计划于2025年9月25日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md)是您访问所有AEM功能的集中式起点。 它根据您的用户角色和您可用的许可证进行个性化，使每个用户能够有效地实现他们的成果。

## AEM的人工智能助手 {#AI-assistant}

适用于AEM的[AI助手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)提供了一个对话界面，旨在让您即时获得与AEM产品相关问题的答案（*可供所有用户使用*）并自动创建支持票证（*可供支持管理员使用*）。 它直接嵌入到AEM中，可从AEM Experience Hub、Cloud Manager和创作UI访问。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#enhancements-sites}

* 在内容片段管理界面中，您现在可以查看内容片段的工作流状态，其中包含关于所选片段的过去和当前正在运行的工作流的详细信息。
* 在常见情况下，通过通过UUID而不是通过路径打开片段，在新的内容片段编辑器中打开内容片段的性能提升了25%。
* 现在，在复制包含引用的片段的内容片段时，引用的片段的副本存储在与父片段副本相同的位置。
* 您现在可以在文件夹设置中配置自定义工作区，以将内容片段导出到Adobe Target中已配置的工作区。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Content Hub 的新功能 {#new-features-content-hub}

**通过筛选器属性进行批量搜索**

Content Hub现在可帮助您更快地发现所需的资源。 借助新的批量搜索功能，您可以为任何筛选器属性输入多个值(以分隔符（例如，多个SKU ID）分隔)，并使用单个搜索即时检索所有匹配的资产。

### 具有 OpenAPI 功能的动态媒体中的新功能 {#new-features-dynamic-media-with-openapi}

**具有OpenAPI URL的SEO友好DM**

在DM中使用OpenAPI创建资产交付的虚URL，将系统生成的长UUID替换为简短的可读标识符。 这使得链接更符合SEO要求，并且更好地与您的品牌或营销活动保持一致。 虚URL在运行时自动解析为原始资产UUID，而不会中断现有工作流。

>[!NOTE]
>
>此功能将在9月10日作为有限可用功能提供。 您可以[创建并提交Adobe客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，以便为您的部署启用它。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* **日期和时间输入组件**：日期和时间组件现已可用，使用户可以使用日历和时钟界面选择日期和时间，或以支持的格式手动输入值。
* [增强了文件上载的错误处理](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)：文件附件组件现在将自动根据允许列表验证上载的文件类型。 如果用户以不支持的格式上传文件，则表单在提交期间显示错误。 该组件还会检查文件内容以验证其类型，从而提高表单的整体安全性。
* **为自定义提交操作指定的错误响应**：当自定义提交操作遇到未处理的错误时，返回错误代码502。 这有助于确定问题与自定义提交操作相关，从而简化调试过程。
* [从记录文档排除隐藏字段](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)：添加了一个新属性，以允许从记录文档排除隐藏字段。 默认情况下，不选中此选项，该选项适用于所有表单字段。

### AEM Forms中的预发行功能

* [生成并同步AFP呈现版本](/help/forms/document-generation-afp-api.md)：您现在可以使用AEM Forms Communication API将XDP文件转换为AFP格式。 AFP是一种广泛应用于大型企业印刷的高性能格式。
* 规则编辑器中的&#x200B;**增强功能**
   * **验证和重置函数增强功能**：验证和重置方法现在支持在面板、字段和表单级别执行。 以前，仅在表单级别支持它们。
   * **现代JavaScript支持**：为自定义函数添加了对ECMAScript 2019及更高版本功能的支持，允许您编写更高效、模块化且可重用的代码
   * **规则编辑器中的“下载DoR选项”**：规则编辑器中已将用于下载记录文档(DoR)的函数作为现成(OOTB)选项添加。
     ![记录文档](/help/forms/assets/document-of-record-rn.gif)
   * **规则编辑器中的动态变量**：您现在可以在规则编辑器中使用动态（临时）变量，以便在定义条件和操作时更加灵活。 不再需要隐藏字段来存储临时值。
   * **规则编辑器中的自定义基于事件的规则**：您现在可以定义自定义事件并根据这些事件触发规则。
   * **上下文感知的可重复面板规则**：在可重复面板中，规则现在基于上下文执行，而不是仅应用于最后一个面板实例。
   * **由参数触发的规则**：规则编辑器现在支持基于查询参数、UTM参数或浏览器参数执行规则。
   * **特定于表单的自定义函数**： Edge Delivery Services Forms现在支持特定于表单的自定义函数脚本，在管理可重用逻辑方面提供了更大的灵活性。
   * **自定义函数的静态导入**：通用编辑器中的规则编辑器现在支持静态导入，允许开发人员跨多个表单组织、共享和重用函数。

### AEM Forms 中的早期采用者功能

* **涂写签名组件**：您现在可以使用涂写签名组件来帮助用户将其签名添加到表单，如协议表单中。 该组件允许用户使用鼠标、手写笔或触摸屏直接在表单中绘制其签名。
* **规则编辑器中的直接API集成**：自适应Forms现在支持可视化规则编辑器中的直接API集成，而无需表单数据模型。 作者可以使用URL或cURL导入来配置API，映射输入/输出参数，以及使用身份验证的安全调用。

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

### JavaScript编译更新 {#javascript-compilation}

默认客户端库(clientlibs) JavaScript编译现在以ECMASCRIPT_2018而不是ECMASCRIPT5为目标。 虽然此更新在过去可以覆盖，但默认情况下，它支持性能改进、现代JavaScript语法和功能。

### 即将弃用Java API {#java-api-deprecation}

多个已弃用的API将于8月31日定向删除，因此不应再引用。 9月初，如果检测到API使用情况，将发送操作中心通知，9月25日之后，将在Cloud Manager构建期间显示通知，强调删除使用情况的重要性。 有关完整的详细信息，请参阅[弃用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，但为了方便起见，下面列出了这些API：

<details>
  <summary>展开以查看Java API的弃用情况</summary>

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

如果由于存在不受支持的依赖项（请参阅 [Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您的环境无法升级，您应该已经收到了 Adobe 发来的电子邮件，其中包含了具体的后续操作步骤。请确保在&#x200B;**2025年10月1日**&#x200B;之前完成所有必需的更新，以便您的环境可以升级而不会中断。

注意：运行时版本与代码的构建版本是分开的。虽然我们建议使用 Java 21 进行构建，但目前仍支持使用 Java 11 进行构建。未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从&#x200B;**9月25日**&#x200B;开始，将忽略任何不受支持的自定义日志记录覆盖。 根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### Edge计算(Beta计划) {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 在授予内容访问权限之前，通过身份标识提供商对用户进行身份验证
* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将来自第三方API的响应传递到浏览器之前，请重新设置响应格式（可能还会聚合多个API响应）
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的 CDN 配置（Beta 计划） {#cdn-eds-beta}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在在Beta版中，您可以为功能部署配置管道，包括CDN源选择器、响应和请求转换、CDN日志转发等。 请联系 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 并提供您的用例详情。

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
