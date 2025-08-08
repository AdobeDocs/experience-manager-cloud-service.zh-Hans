---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: e9aef80c162d681894cff53f65bd9f0bc7afd948
workflow-type: tm+mt
source-wordcount: '2235'
ht-degree: 49%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.7.0)的发布日期是2025年8月7日。 下一个功能版本(2025.8.0)计划于2025年8月28日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440930?quality=12&captions=chi_hans)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#enhancements-sites}

* 现在，您可以在一次操作中复制具有引用的片段（子项）的内容片段。 这允许重复使用现有的内容片段结构来创建新内容。
* 在内容片段管理UI中，您现在可以查看内容片段的工作流状态，以及有关所选片段过去和当前运行的工作流的详细信息。
* 重命名或移动Live Copy源页面现在会触发重新发布相应地重命名或移动的Live Copy页面。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**将形状添加到Dynamic Media模板**

您现在可以[将形状图层添加到Experience Manager Assets中的Dynamic Media模板](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas)。 与图像和文本图层类似，形状图层也支持通过模板URL进行实时更新的参数。 您还可以在模板中包含指向形状的call-to-action (CTA)链接。

![向Dynamic Media模板添加形状](/help/assets/assets/enable-uniform-radius-shape.png)

**AI生成的元数据增强**

AEM Assets现在使您能够[在“资源浏览”页面的“卡片视图”或“列表视图”中](/help/assets/smart-tags.md#configure-ai-generated-titles)配置资源标题的显示。 您可以选择显示您定义的资源标题、使用AI生成的标题，或者仅在资源没有现有标题时使用人工智能生成的标题。

![配置AI生成的标题](/help/assets/assets/configure-title-ai-generated.png)

您现在还可以选择在文件夹级别禁用AI生成的元数据。


### Content Hub 的新增强功能 {#new-features-content-hub}

**在Content Hub中增强了品牌灵活性**

在现有个性化功能的基础上，Content Hub现在允许管理员通过添加自定义徽标图像来进一步定制其部署。 还增加了对TIFF文件格式的支持，用于横幅和徽标图像，从而实现了更大的设计灵活性。

**与标题链接更智能地共享**

现在，无论是在资源详细信息视图中，还是在选择一个或多个资源后，您都可以在生成共享链接时添加标题。 这有助于收件人轻松识别每个链接的用途，尤其是在接收多个共享资产时。

![私有和公共链接](/help/assets/assets/shared-link-for-assets.png)

**已改进筛选器导航**

Content Hub现在在筛选器中包括&#x200B;**显示所有**&#x200B;选项，允许用户查看所有可用彩块以及资源计数，而当前限制是最多只能查看十个彩块。 每个过滤器中的增强搜索和排序功能使更轻松地更高效地发现和管理资源。

### AEM桌面应用程序3.0.0版 {#desktop-app-release-3.0.0}

享受新文件和文件夹的自动上传、增强的文件操作、更智能的资源发现以及与AEM的无缝集成 — 使内容管理更快、更清晰、更直观。

有关完整的功能列表，请参阅[桌面应用程序发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/release-notes)。

### 具有OpenAPI功能的Dynamic Media的新增功能 {#new-features-dynamic-media-with-openapi}

**发布前预览资源**

[!DNL Dynamic Media with OpenAPI capabilities]现在允许直接在[!DNL AEM Sites]创作页面中预览资产，然后再将其公开。 与利益相关者共享预览页面，以收集关于视觉质量和上下文适应的反馈。 在审核周期中，您可以创建和管理多个资源版本，然后再最终确定它们以供发布。

**针对OpenAPI图像请求的增强型智能成像**

现在，所有OpenAPI图像请求都可充分利用具有自动促销和回退逻辑的智能成像。 此增强功能根据设备和网络条件优化图像，从而加快页面加载速度并减少带宽使用量，同时保持视觉质量。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-features}

**自适应Forms和表单片段的通用编辑器**

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)现在支持创建自适应Forms和可重用的表单片段。 内容作者可在简化的所见即所得（WYSIWYG）创作环境中，以可视化方式构建表单、配置提交操作，并添加 reCAPTCHA 验证。此功能可加快表单创建流程，提升一致性，并增强对垃圾信息及自动滥用行为的防护能力。

![通用编辑器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


适用于Edge Delivery Services Forms的&#x200B;**Forms提交服务**

请参阅[Forms提交服务](/help/forms/forms-submission-service.md)。 允许您将自适应表单提交的数据无缝地直接存储到流行的电子表格平台，如Google Sheets、Microsoft OneDrive或SharePoint。 此集成允许将表单数据直接提交到您选择的电子表格，从而简化数据管理，消除手动数据传输并减少错误。

主要优势包括：

* **直接集成：**&#x200B;将表单配置为将数据直接提交到指定的电子表格。
* **自定义数据映射：**&#x200B;将表单字段映射到相应的电子表格列，以便进行有组织的存储。
* **访问控制：**&#x200B;利用现有的电子表格权限来管理谁可以访问或修改提交的数据。

**从自适应Forms生成并同步AFP演绎版**

[AFP Output Sync API](/help/forms/document-generation-afp-api.md)使管理员和用户能够从Adaptive Forms生成AFP（高级函数演示）输出，并将输出与外部系统或存储位置同步。 AFP 是一种专为打印优化的高性能文档格式，常用于大型企业环境。

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

### AEM Forms中的新增抢先访问功能 {#forms-new-early-access-features}

AEM Forms早期访问计划为您提供独一无二的机会，让您能够访问前沿创新并帮助形成其发展。

这些发行说明列出了当前版本中提供的创新。 有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。


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

使用直观的点击式界面，直接在文档中构建动态的数据驱动操作。 轻松定义条件逻辑、自动化工作流并个性化内容，而无需编写代码。

自定义组件的&#x200B;**AEM Forms Scaffolder CLI**

>[!VIDEO]&#x200B;(https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms开发工具)

使用此CLI工具加速AEM Forms Edge Delivery Services开发。 即时生成启动自定义组件开发所需的代码和布线 — 无样板，轻松无忧。

用于动态表单数据的&#x200B;**API集成工具**

利用API集成工具，表单作者可以创建动态、智能的表单，这些表单会根据用户交互自动从外部REST API获取和填充数据。 这种无代码集成功能将静态表单转换为响应式数据收集界面。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

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

**Java 11运行时* — 现已弃用，并且大多数环境都已升级到性能更高的&#x200B;**&#x200B;Java 21运行时**。

如果由于存在不受支持的依赖项（请参阅 [Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您的环境无法升级，您应该已经收到了 Adobe 发来的电子邮件，其中包含了具体的后续操作步骤。请确保在 **2025 年 8 月 28 日**&#x200B;之前完成所有必要的更新，以确保您的环境能够在不受干扰的情况下进行升级。

注意：运行时版本与代码的构建版本是分开的。虽然我们建议使用 Java 21 进行构建，但目前仍支持使用 Java 11 进行构建。未来将另行发布针对 Java 11 版本的弃用通知。

### AEM Java 日志配置策略的执行 {#logconfig-policy}

正如4月发布说明中所述，AEM Java 日志必须遵循标准格式，以确保在所有客户环境中进行可靠监控。自定义日志配置（如更改日志格式、输出文件或默认日志级别）已不再受支持。日志必须继续定向到默认文件，且必须保留 AEM 产品代码的默认日志级别。请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)，以了解完整详情。

从 **8 月下旬**&#x200B;开始，任何不受支持的自定义日志记录覆盖都将被忽略。根据我们的分析，大多数客户不会受到影响，对于当前配置可能受到影响的任何客户，Adobe 将会与其联系。

请审查并更新所有依赖自定义日志记录行为的下游流程。例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整您的摄取规则。
* 如果您之前通过更改日志级别来降低日志详细程度，请注意，恢复默认级别可能会增加日志量。

### 默认清除旧版本和审计日志 {#mt-defaults}

目前，内容版本和审核日志在默认情况下禁用其关联的*清除维护任务，因此除非明确配置，否则不会删除任何数据。

但是，为优化存储库性能，默认情况下，将在未来宣布的日期启用清除，遵循以下准则：

#### 内容版本 {#mt-content}

* **新环境*-(在即将到来的日期之后创建（稍后通知）
   * 将定期删除早于**30天* — 的版本。
   * 保留过去30天内最新的五个版本，以及最新版本和当前版本，无论其历史时间如何。

* **现有环境* — （在此即将到来的日期之前创建）：
   * 将定期删除早于**7年* — 的版本。
   * 过去 7 年内的所有版本均予以保留。
   * 这个较高的默认阈值可防止意外移除最近的数据。但是，建议配置较低的值以优化存储库性能。

* 您可以通过使用配置管道部署的 YAML 配置来修改这些默认值。

#### 审核日志 {#mt-auditlogs}

* **新环境* — （在即将到来的日期之后创建，将单独通知）：
   * 将定期删除早于**7天* — 的复制、DAM和页面审核日志。
   * 默认情况下，所有事件都会被记录。

* **现有环境* — （在此即将到来的日期之前创建）：
   * 将定期删除早于**7年* — 的复制、DAM和页面审核日志。
   * 默认情况下，所有事件都会被记录。
   * 这个较高的默认阈值可防止意外移除最近的数据。但是，建议配置较低的值以优化存储库性能。

* 您可以通过使用配置管道部署的 YAML 配置来修改这些默认值。

有关更多详细信息，请参阅[维护任务文章](/help/operations/maintenance.md#defaults)。

### 边缘计算（Alpha 计划） {#edge-computing}

边缘计算允许您在内容传递网络 (CDN) 层执行 JavaScript，使数据处理更接近最终用户。这降低了延迟，使得边缘设备能够提供响应迅速、动态丰富的体验。

常见的用例包括：

* 在授予内容访问权限之前，通过身份标识提供商对用户进行身份验证
* 根据地理位置、设备类型或用户属性对内容进行个性化设置
* 充当 CDN 与您的源站之间的中间件
* 在将第三方 API 的响应（可能还包括聚合多个 API 的响应）传递给浏览器之前，对其进行重新格式化
* 使用从各种后端拼接的内容，在边缘构建并呈现服务器渲染的 HTML
* 为ChatGPT和Claude等LLM公开MCP服务器以访问自定义工具

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的 CDN 配置（Beta 计划） {#cdn-eds-beta}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在在Beta版中，为包括CDN源选择器、响应和请求转换、CDN日志转发等功能部署配置管道。 请联系 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 并提供您的用例详情。

### RDE快照(Alpha计划) {#rde-snapshot-beta}

在Alpha中，快速开发环境(RDE)现在支持一种功能，可拍摄代码和内容的当前状态的快照，以后可以恢复。 在同步可能需要还原的代码或在开发不同功能之间切换时，这可能会很有用。 也可以仅恢复可变内容作为测试的已知起点。

如果对此功能有兴趣提供反馈，请发送电子邮件至[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 日志转发至更多目标（Beta 项目） {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

现在处于Beta阶段，您可以将AEM日志转发到Amazon S3、Sumo Logic、Dynatrace以及您自己的New Relic帐户(而不是Adobe提供的帐户)。 请注意，这些日志记录目标支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

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
