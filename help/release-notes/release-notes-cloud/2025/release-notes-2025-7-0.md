---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.7.0 版的发行说明。'
feature: Release Information
role: Admin
exl-id: b1d25db0-d4a8-4663-b7fe-2d7381e12567
source-git-commit: 76ccdf13f56d7020ef266bc54bebbcc6eff1067d
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.7.0 版的发行说明 {#release-notes}

以下部分概述了 2025.7.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.7.0) 的发布日期为 2025 年 8 月 7 日。下一个功能版本 (2025.8.0) 计划于 2025 年 8 月 28 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#enhancements-sites}

* 现在，您可以在一次操作中复制内容片段及其引用的片段（子片段）。这样就可以重复使用现有的内容片段结构来创建新内容。
* 在内容片段管理界面中，您现在可以查看内容片段的工作流状态，其中包含关于所选片段的过去和当前正在运行的工作流的详细信息。
* 现在，重命名或移动实时副本的源页面将触发重新发布相应的被重命名或被移动的实时副本页面。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**将形状添加到动态媒体模板**

您现在可以在 Experience Manager Assets 中[将形状图层添加到动态媒体模板](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas)。与图像和文本图层类似，形状图层支持使用参数通过模板 URL 进行实时更新。您还可以在模板的形状中添加行动号召 (CTA) 链接。

![将形状添加到动态媒体模板](/help/assets/assets/enable-uniform-radius-shape.png)

**AI 生成的元数据增强功能**

现在，AEM Assets 允许您在资产浏览页面上[配置卡片视图或列表视图中资产标题的显示方法](/help/assets/smart-tags.md#configure-ai-generated-titles)。您可以选择显示您定义的资产标题、用 AI 生成的标题，或者仅在资产缺少标题时使用 AI 生成的标题。

![配置 AI 生成的标题](/help/assets/assets/configure-title-ai-generated.png)

您现在还可以选择在文件夹级别禁用 AI 生成的元数据。

### Content Hub 的新功能 {#new-features-content-hub}

**增强了 Content Hub 中的品牌化灵活性**

在现有的个性化功能的基础上，Content Hub 现在允许管理员通过添加自定义徽标图像来进一步定制他们的部署。还为横幅和徽标图像增加了对 TIFF 文件格式的支持，有助于更大的设计灵活性。

**通过带标题的链接促进共享**

现在，您可以在生成共享链接时添加一个标题——可以从资产详细信息视图中添加或者在选择一个或多个资产后。这有助于接收者轻松识别每个链接的用途，尤其是在接收多个共享资产时。

![专用和公开链接](/help/assets/assets/shared-link-for-assets.png)

**改进了过滤器导航**

现在，Content Hub 在过滤器中包含一个&#x200B;**显示全部**&#x200B;选项，允许用户查看所有可用的方面以及资产数量，而当前限制只能查看最多十个方面。增强了每个过滤器中的搜索和排序功能，使用户可以更轻松、更有效地发现和管理资产。

### AEM 桌面应用程序发行版本 3.0.0 {#desktop-app-release-3.0.0}

愉快地使用新文件和文件夹的自动上传、改进的文件操作、更佳的资产浏览以及与 AEM 的无缝集成——有助于更快、更清晰、更直观地管理内容。

完整的功能列表请参阅[桌面应用程序发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/release-notes)。

### 具有 OpenAPI 功能的动态媒体中的新功能 {#new-features-dynamic-media-with-openapi}

**发布前预览资产**

[!DNL Dynamic Media with OpenAPI capabilities] 现在允许直接在 [!DNL AEM Sites] 作者页面中预览资产，然后再将其公布。与利益相关者共享预览页面，以收集有关外观质量和上下文适应度的反馈。在审阅周期内，您可以在最终发布之前创建和管理多个资产版本。

**为 OpenAPI 图像请求增强了智能成像**

现在，所有 OpenAPI 图像请求都充分利用具有自动提升和回退逻辑的智能成像功能。此增强功能可根据设备和网络条件优化图像，提供更快的页面加载速度，并减少带宽使用——同时保持视觉质量。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

**用于自适应表单和表单片段的通用编辑器**

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)现在支持自适应表单创建和可重复使用的表单片段。内容作者可在简化的所见即所得（WYSIWYG）创作环境中，以可视化方式构建表单、配置提交操作，并添加 reCAPTCHA 验证。此功能可加快表单创建流程，提升一致性，并增强对垃圾信息及自动滥用行为的防护能力。

![通用编辑器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**Edge Delivery Services Forms 的表单提交服务**

参见[表单提交服务](/help/forms/forms-submission-service.md)。允许您将自适应表单提交的数据无缝地直接存储到流行的电子表格平台中，例如 Google Sheets、Microsoft OneDrive 或 SharePoint。这一集成方式将表单数据直接提交到您选择的电子表格，从而简化了数据管理，消除了手动数据传输方法，减少了错误。

主要优势包括：

* **直接集成：**&#x200B;配置您的表单，将数据直接提交到指定的电子表格。
* **自定义数据映射：**&#x200B;将表单字段映射到相应的电子表格列，有条理地存储。
* **访问控制：**&#x200B;使用现有的电子表格权限来管理谁可以访问或更改已提交的数据。

**从自适应表单生成并同步 AFP 演绎版**

[AFP 输出同步 API](/help/forms/document-generation-afp-api.md) 使管理员和用户能够从自适应表单生成 AFP（高级功能呈现）输出，并将该输出与外部系统或存储位置同步。AFP 是一种专为打印优化的高性能文档格式，常用于大型企业环境。

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### AEM Forms 中新的早期访问功能 {#forms-new-early-access-features}

AEM Forms 早期访问计划为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

这些发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**交互式通信编辑器的规则编辑器**

使用直观的点击界面直接在文档中构建数据驱动的动态操作。无需编写代码，轻松定义条件逻辑、自动化工作流、个性化内容。

**用于自定义组件的 AEM Forms Scaffolder CLI**

>[!VIDEO](https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms development tool)

使用此 CLI 工具加快您的 AEM Forms Edge Delivery Services 开发。立即生成启动自定义组件开发所需的代码和连接——无需样板，毫无麻烦。

**动态表单数据的 API 集成工具**

API 集成工具使表单作者能够创建可根据用户交互自动从外部 REST API 获取和填充数据的动态、智能的表单。这种无代码集成功能可以将静态表单转换为响应式数据收集界面。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 用于权限管理的节点视图 {#node-view}

AEM 引入了节点视图权限管理。主要功能与经典用户界面一样，但更加友好和高效。请参阅[专用文章](/help/security/touch-ui-principal-view.md)，了解更多信息。

### 更新的弃用流程 {#updated-deprecation-process}

Adobe 会定期审查功能、库、API 和配置，以确保它们符合性能、安全和价值方面的标准。当功能不再满足这些标准时，它们将被标记为弃用，且必须在指定的移除日期前停止使用。在此日期之前，Adobe 将通过电子邮件通知提醒客户，并告知客户在继续或部署新版本之前需要在 Cloud Manager 中采取的行动。若未能采取必要行动，则可能无法升级至 AEM 的新版本，进而对安全性、性能、可靠性和可用性造成潜在影响。

请参阅[弃用文章](/help/release-notes/deprecated-removed-features.md)，以了解更多信息。

#### 即将移除的已弃用 Java API 和 OSGi 配置 {#deprecated-near-removals}

展开下方列表，查看已弃用且不得再使用的 API 和 OSGi 配置。如需了解全部详情（包括移除时间表），请参阅弃用文章。

<details>
  <summary>展开以查看弃用内容</summary>

Java API：

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

OSGi 属性：

* `org.apache.sling.commons.log.LogManager`（所有属性）
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Java 11 运行时弃用 {#java11-runtime-deprecation}

**Java 11 运行时环境*- 现已弃用，大多数环境已经升级到性能更高的 &#x200B;** Java 21 运行时环境**。

如果由于存在不受支持的依赖项（请参阅 [Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您的环境无法升级，您应该已经收到了 Adobe 发来的电子邮件，其中包含了具体的后续操作步骤。请确保在 **2025 年 8 月 28 日**&#x200B;之前完成所有必要的更新，以确保您的环境能够在不受干扰的情况下进行升级。

注意：运行时版本与代码的构建版本是分开的。虽然我们建议使用 Java 21 进行构建，但目前仍支持使用 Java 11 进行构建。未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从 **8 月下旬**&#x200B;开始，任何不受支持的自定义日志记录覆盖都将被忽略。根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### 默认清除旧版本和审计日志 {#mt-defaults}

目前，内容版本和审计日志的相关&#x200B;*清除维护任务*&#x200B;默认处于禁用状态，因此除非进行明确配置，否则不会删除任何数据。

但是，为了优化存储库性能，在将来宣布的日期将默认启用清除。

有关更多详细信息，请参阅[维护任务文章](/help/operations/maintenance.md#defaults)。

#### 内容版本 {#mt-content}

* **新环境**（在即将到来的日期之后创建，稍后将进行沟通）：
   * 将定期删除超过30天的版本。
   * 保留过去30天内最新的五个版本，以及最新版本和当前版本，无论其历史时间如何。

* **现有环境**（在此即将到来的日期之前创建）：
   * 超过7年的版本将定期删除。
   * 过去 7 年内的所有版本均予以保留。
   * 这个较高的默认阈值可防止意外移除最近的数据。但是，建议配置较低的值以优化存储库性能。

* 您可以通过使用配置管道部署的 YAML 配置来修改这些默认值。

#### 审核日志 {#mt-auditlogs}

* **新环境**（在即将到来的日期之后创建，具体日期将另行通知）：
   * 将定期删除超过7天的复制、DAM和页面审核日志。
   * 默认情况下，所有事件都会被记录。

* **现有环境**（在此即将到来的日期之前创建）：
   * 将定期删除超过7年的复制、DAM和页面审核日志。
   * 默认情况下，所有事件都会被记录。
   * 这个较高的默认阈值可防止意外移除最近的数据。但是，建议配置较低的值以优化存储库性能。

* 您可以通过使用配置管道部署的 YAML 配置来修改这些默认值。

### 边缘计算（Alpha 计划） {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 在授予内容访问权限之前，通过身份标识提供商对用户进行身份验证
* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，对其进行重新格式化
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为 ChatGPT 和 Claude 等 LLM 公开 MCP 服务器，以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的 CDN 配置（Beta 计划） {#cdn-eds-beta}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在在 beta 版中，为 CDN 源选择器、响应和请求转换、CDN 日志转发等功能部署配置管道。请联系 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 并提供您的用例详情。

### RDE 快照（Alpha 程序） {#rde-snapshot-beta}

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
