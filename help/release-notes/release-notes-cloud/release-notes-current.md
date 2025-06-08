---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 1b6316d07153fdf93481a252173334af45137a29
workflow-type: tm+mt
source-wordcount: '2062'
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


[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.5.0)的发布日期是2025年6月5日。 下一个功能版本(2025.6.0)计划于2025年6月26日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI生成的元数据**

AEM Assets现在使用[AI自动生成元数据，包括标题、描述和关键字](/help/assets/metadata-assets-view.md#ai-smart-tags)。 这些AI生成的字段可提高元数据的准确性，使资源更易于搜索、分类和推荐。 此方法不仅通过消除手动标记而提高了效率，而且确保了跨大量数字内容的一致性和可扩展性。

![AI生成的元数据](/help/assets/assets/enhanced-smart-tags.png)

**与Figma集成**

AEM Assets与Figma原生集成，允许设计人员从Figma用户界面中直接访问AEM Assets中存储的资源。 您可以将AEM Assets中管理的内容放在Figma画布中，然后在AEM Assets存储库中保存新内容或编辑的内容。

![与Figma集成](/help/assets/assets/figma-integration.png)


### Content Hub中的新增功能 {#new-features-content-hub}

**基于属性的访问控制(ABAC)**

[Content Hub现在允许您应用基于规则的限制来访问资源](/help/assets/attribute-based-access-control.md)。 资源权限可确保治理，还可确保用户只能访问相关的资源。

资源限制规则基于元数据，如果规则中定义的条件与资源元数据匹配，则资源将向用户组显示。

基于属性的访问控制的一些主要优势包括：

* 消除权限对文件夹结构的依赖性

* 允许管理员上传资源并追溯确定权限结构

* 减少重复项数量 — 提高资源完整性。 当同一资产与不同组共享时，基于文件夹的权限需要重复项。

**UI品牌**

Content Hub现在允许管理员[使用特定于品牌的元素](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub)自定义用户界面，这些元素包括横幅图像、横幅标题和正文文本以及主要颜色和次要颜色。 这些增强功能有助于确保品牌一致性、简化用户登录和建立信任。

![UI品牌](/help/assets/assets/content-hub-ui-branding.png)

**公共链接共享**

Content Hub现在支持[生成可共享链接，以允许没有应用程序访问权限的外部用户](/help/assets/share-assets-content-hub.md##share-assets)查看资源元数据或下载资源。

![UI品牌](/help/assets/assets/public-and-private-link.png)

**收藏集管理**

Content Hub现在允许您[在创建过程中控制对收藏集的访问，确保只有授权用户才能查看或管理分组的资源](/help/assets/collections-content-hub.md##create-collections)。 它可确保改进的安全性、更好的协作、有条理的资产管理和简化的治理。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>收藏集治理是一项受限制的可用性功能。 您可以通过创建支持票证来启用它。

**以ZIP格式下载多个资产**

Content Hub现在还允许您[将所选资源及其演绎版](/help/assets/download-assets-content-hub.md#download-asset-renditions)下载到ZIP文件中，而不是作为单独的文件来为您简化文件管理。

在Content Hub中&#x200B;**Dynamic Media演绎版**

直接在Content Hub用户界面](/help/assets/download-assets-content-hub.md#download-asset-renditions)中访问所有[Dynamic Media预设演绎版和智能裁剪以供下载。

![&#x200B;Dynamic Media演绎版](/help/assets/assets/dm-renditions-content-hub.png)

### Dynamic Media中的新增功能 {#new-features-dynamic-media}

**Dynamic Media与AJO B2C的本机集成&#x200B;**

[Experience Manager (AEM) Dynamic Media与Journey Optimizer (AJO) B2C](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/combine/aem-dynamic)的本机集成，使营销人员能够轻松地将AEM Dynamic Media资产（演绎版和DM模板）嵌入到AJO内容中，并在各个渠道中提供实时更新和超个性化体验。

>[!VIDEO](https://video.tv.adobe.com/v/3457695/?learn=on&enablevpops=&autoplay=true)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 预发行版功能

* [通用编辑器 - 表单片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：通用编辑器现在允许您为自适应表单创建和重复使用表单片段。这些片段是可重复使用的表单部分（例如，联系方式、同意字段），只需构建一次即可应用于多个表单。此功能简化了表单创建，确保了一致性，提高了创作效率。

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

Forms 与 AEP 的集成功能现在可供早期采用者使用。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 更新了弃用流程 {#updated-deprecation-process}

Adobe会定期审查功能、库、API和配置，以确保它们符合性能、安全性和价值标准。 当功能不再符合这些标准时，将标记它们以供弃用，并且必须在指定的删除日期之前停止使用。 在此日期之前，Adobe将通过电子邮件通知提醒客户，以及在继续使用或部署新内部版本之前需要在Cloud Manager中执行的操作。 如果未能采取必要措施，可能会导致无法升级到新版本的AEM，进而可能对安全性、性能、可靠性和可用性造成影响。

有关详细信息，请参阅[弃用文章](/help/release-notes/deprecated-removed-features.md)。

#### 已弃用的Java API和OSGi配置接近删除日期 {#deprecated-near-removals}

展开以下列表以查看不再使用的已弃用API和OSGi配置。 有关完整的详细信息（包括删除时间线），请参阅弃用文章。

<details>
  <summary>展开以查看弃用项</summary>

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

OSGi属性：

* `org.apache.sling.commons.log.LogManager` （所有属性）
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`， `org.apache.sling.commons.log.pattern`)

</details>

### 弃用Java 11运行时 {#java11-runtime-deprecation}

**Java 11运行时**&#x200B;现已弃用，并且大多数环境已升级到性能更高的&#x200B;**Java 21运行时**。

如果由于不支持的依赖项而无法升级环境（请参阅[Java 21运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您应该已经收到来自Adobe的电子邮件，其中包含具体的后续步骤。 请确保在&#x200B;**2025年8月28日**&#x200B;之前完成所有必需的更新，以便您的环境可以升级而不会中断。

注意：运行时版本与代码的内部版本不同。 虽然我们建议使用Java 21进行构建，但目前仍支持Java 11内部版本。 未来将共享有关Java 11内部版本的单独弃用通知。

### 实施AEM Java日志配置策略 {#logconfig-policy}

如4月发行说明中所述，AEM Java日志必须遵循标准格式，以确保在所有客户环境中进行可靠的监控。 不再支持自定义日志配置，如更改日志格式、输出文件或默认日志级别。 日志必须保持定向到默认文件，并且必须保留AEM产品代码的默认日志级别。 请参阅[日志记录文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)中的完整详细信息。

从&#x200B;**8月底**&#x200B;开始，任何不受支持的自定义日志记录覆盖都将被忽略。 根据我们的分析，大多数客户不会受到影响，Adobe将直接联系任何其当前配置可能受到影响的客户。

请检查并更新依赖自定义日志记录行为的任何下游进程。 例如：

* 如果您的日志转发系统需要自定义日志格式，您可能需要调整摄取规则。
* 如果您之前通过更改日志级别降低了日志详细程度，请注意，恢复到默认级别可能会增加日志量。

### 默认清除旧版本和审核日志 {#mt-defaults}

目前，内容版本和审核日志在默认情况下禁用其关联的&#x200B;*清除维护任务*，因此除非通过它们各自的OSGi属性明确配置，否则不会删除任何数据。

但是，为优化存储库性能，从2025年6月下旬&#x200B;**开始**，默认情况下将按照以下准则启用清除：

#### 内容版本 {#mt-content}

* **新环境** (在即将到来的日期之后创建（稍后通知）
   * 将定期删除超过&#x200B;**30天**&#x200B;的版本。
   * 会保留过去30天内的最近五个版本，以及最新版本和当前版本，而不考虑其存在时间。

* **现有环境** （在此即将到来的日期之前创建）：
   * 将定期删除超过&#x200B;**7年**&#x200B;的版本。
   * 过去7年内的所有版本都将保留。
   * 此高默认阈值可防止意外删除最近的数据。 但是，建议配置较低的值以优化存储库性能。

* 您可以通过OSGi配置覆盖来修改这些默认值。

#### 审核日志 {#mt-auditlogs}

* **新环境**（在即将到来的日期之后创建，将单独通知）：
   * 将定期删除超过&#x200B;**7天**&#x200B;的复制、DAM和页面审核日志。
   * 默认情况下，将记录所有事件。

* **现有环境** （在此即将到来的日期之前创建）：
   * 将定期删除超过&#x200B;**7年**&#x200B;的复制、DAM和页面审核日志。
   * 默认情况下，将记录所有事件。
   * 此高默认阈值可防止意外删除最近的数据。 但是，建议配置较低的值以优化存储库性能。

* 您可以通过OSGi配置覆盖来修改这些默认值。

有关更多详细信息，请参阅[维护任务文章](/help/operations/maintenance.md#defaults)。

### Edge计算(Alpha计划) {#edge-computing}

Edge计算允许您在CDN层执行JavaScript，使数据处理更接近于最终用户。 这减少了延迟，并可在边缘实现响应式动态体验。

常见的用例包括：

* 在授予对内容的访问权限之前，使用身份提供程序验证用户
* 根据地理位置、设备类型或用户属性个性化内容
* 充当CDN与您的来源之间的中间件
* 在将来自第三方API的响应交付给浏览器之前，重新设置响应格式（可能聚合多个API响应）
* 使用从各种后端拼合的内容，在边缘构成并提供服务器渲染的HTML

我们为实时生产站点的AEM Publish Delivery或Edge Delivery Services项目提供的机会有限。 如果您有兴趣参与或想了解更多信息，请发送电子邮件至[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，并提供您用例的简短描述。

### Edge Delivery Services (Beta计划)的CDN配置 {#cdn-eds-beta}

Adobe-Managed CDN提供了灵活的配置选项，如[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。

现在在Beta版中，为包括CDN源选择器、响应和请求转换等功能部署配置管道。 请联系[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com)以了解您的用例的详细信息。

### AEM日志转发到更多目标(Beta程序) {#log-forwarding-beta}

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM已支持AEM和CDN将日志转发到Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和OpenSearch）以及Splunk。 此功能以自助方式配置，并使用配置管道进行部署。

现在处于Beta阶段，您可以将AEM日志转发到Amazon S3、Sumo Logic和您自己的New Relic帐户(而不是Adobe提供的帐户)。 请注意，这些日志记录目标支持AEM日志(包括Apache/Dispatcher)，但CDN日志不支持。 发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

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
