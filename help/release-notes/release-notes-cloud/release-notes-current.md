---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: b4aec70b13575366c1d40ccf935481580a1fb6d8
workflow-type: ht
source-wordcount: '1810'
ht-degree: 100%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.6.0) 的发布日期为 2025 年 6 月 26 日。下一个功能版本 (2025.7.0) 计划于 2025 年 8 月 7 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**在资源视图中增强了元数据表单管理功能。**

您现在可以直接从管理视图将元数据表单导入至资源视图。在资源视图中对这些表单所做的任何更新都会自动同步至管理视图，确保两个视图之间的一致性。此功能支持无缝过渡至新版资源视图，同时保持现有元数据配置的连续性。

![AI 生成的元数据](/help/assets/assets/import-metadata-forms-page.png)

### Content Hub 的新增强功能 {#new-features-content-hub}

**收藏集治理**

Content Hub 现在允许您[在创建过程中控制对收藏集的访问权限，确保只有授权用户才能查看或管理分组资产](/help/assets/collections-content-hub.md##create-collections)。它确保了安全性的提升、协作的优化、资产管理的有序化以及治理的简化。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}



### 预发行版功能

* [适用于自适应表单与表单片段的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：通用编辑器现已支持创建自适应表单及可重复使用的表单片段。内容作者可在简化的所见即所得（WYSIWYG）创作环境中，以可视化方式构建表单、配置提交操作，并添加 reCAPTCHA 验证。此功能可加快表单创建流程，提升一致性，并增强对垃圾信息及自动滥用行为的防护能力。

* [从自适应表单生成并同步 AFP 演绎版](/help/forms/document-generation-afp-api.md)：AFP 输出同步 API 使管理员和用户能够从自适应表单生成 AFP（高级功能呈现）输出，并将该输出同步至外部系统或存储位置。AFP 是一种专为打印优化的高性能文档格式，常用于大型企业环境。

* [SharePoint 文档库 - 使用原始文件名保存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：现在，您可以选择使用表单附件的原始文件名将其保存在 SharePoint 文档库中。此增强功能简化了上传文件的识别和管理。

* **规则编辑器**：
   * [“When”子句中带有单击事件的二进制条件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：规则编辑器现在允许您在“When”子句中将按钮单击事件（_Is Clicked_）与其他条件相结合。这样就可以根据用户交互和其他因素更精确地控制规则的执行。注意：如果使用多个条件，单击事件必须是列出的第一个条件。
   * [字段和面板的验证条件](/help/forms/rule-editor-core-components-usecases.md)：规则编辑器现在包括 _IsValid_ 和 _IsNotValid_ 两个条件。这些条件允许您检查特定字段或整个面板（包括水平选项卡、垂直选项卡、可折叠项和向导等布局方法）的验证状态，从而根据验证结果改善表单导航和用户体验。
* [改进了 SharePoint 列表的范围管理](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint 网站现在支持所有管理路径，例如 /sites 和 /teams。这一增强功能有助于更加广泛地集成不同的 SharePoint 网站结构，为连接组织内容提供了更大的灵活性。
* [支持将记录文档保存到 SharePoint 列表](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：使用基于 SharePoint 列表的表单数据模型 (FDM) 创建的表单现在可以通过配置记录文档绑定引用字段属性将记录文档 (DoR) 保存到 SharePoint 列表。此增强功能可将受支持的表单数据和文档与 SharePoint 存储无缝集成。

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP) 与 Forms 集成

* [AEM Forms 与 Adobe Experience Platform 的集成](/help/forms/aem-forms-aep-connector.md)：AEM Forms 到 Adobe Experience Platform 的连接器可实现自适应表单与 Adobe Experience Platform 之间的无缝集成。此功能可将表单数据映射至 XDM 架构，并实时提交至 Adobe Experience Platform（AEP）。该功能简化了数据采集流程，有助于在 Adobe Experience Cloud 各项解决方案中实现个性化与激活等应用场景。

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

**Java 11 运行时环境**&#x200B;现已弃用，大多数环境已经升级到性能更高的 **Java 21 运行时环境**。

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

然而，为了优化存储库性能，从 **2025 年 7 月上旬**&#x200B;开始，将默认启用清除功能，并遵循以下指南：

#### 内容版本 {#mt-content}

* **新环境**（在即将到来的日期（稍后通知）之后创建）
   * 超过&#x200B;**30 天**&#x200B;的版本将定期被删除。
   * 保留过去30天内最新的五个版本，以及最新版本和当前版本，无论其历史时间如何。

* **现有环境**（在此即将到来的日期之前创建）：
   * 超过&#x200B;**7 年**&#x200B;的版本将定期被删除。
   * 过去 7 年内的所有版本均予以保留。
   * 这个较高的默认阈值可防止意外移除最近的数据。但是，建议配置较低的值以优化存储库性能。

* 您可以通过使用配置管道部署的 YAML 配置来修改这些默认值。

#### 审核日志 {#mt-auditlogs}

* **新环境**（在即将到来的日期之后创建，具体日期将另行通知）：
   * 超过 **7 天**&#x200B;的复制、DAM 和页面审计日志将定期删除。
   * 默认情况下，所有事件都会被记录。

* **现有环境**（在此即将到来的日期之前创建）：
   * 超过 **7 年**&#x200B;的复制、DAM 和页面审计日志将定期删除。
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

我们为实时生产站点提供的 AEM Publish Delivery 或 Edge Delivery Services 项目的机会数量有限。如果您有兴趣参与或想了解更多信息，请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) 并简要描述您的用例。

### Edge Delivery Services 的 CDN 配置（Beta 计划） {#cdn-eds-beta}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在处于 beta 阶段，为包括 CDN 源选择器、响应和请求转换等功能部署配置管道。请联系 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 并提供您的用例详情。

### AEM 日志转发至更多目标（Beta 项目） {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

目前处于 beta 阶段，您可以将 AEM 日志转发到 Amazon S3、Sumo Logic 以及您自己的 New Relic 账户（非 Adobe 提供的账户）。请注意，这些日志记录目标支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

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
