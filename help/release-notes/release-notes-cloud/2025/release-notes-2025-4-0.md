---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.4.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.4.0 版的发行说明。'
feature: Release Information
role: Admin
exl-id: 48e09824-5c67-49d8-8896-358d679649fc
source-git-commit: c8391e09b7e2888423187f48360423c52b18fe0a
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.4.0 版的发行说明 {#release-notes}

以下部分概述了 2025.4.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.4.0) 的发布日期为 2025 年 4 月 24 日。下一个功能版本 (2025.5.0) 计划于 2025 年 6 月 5 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看 2025 年 4 月发布概述视频，了解 2025.4.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3464012?quality=12&captions=chi_hans)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#enhancements-sites}

**新的内容片段模型管理用户界面**

进一步完善了使用 AEM 内容片段时的新客户端用户界面的列表，现在为内容片段模型提供一个新的管理用户界面。新的用户界面提供了一个简洁、现代的列表视图，允许使用过滤器搜索模型，并显示模型标记以及存在哪些基于特定模型的内容片段。文档请参见[这里](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**增强安全性环境不支持 Dynamic Media (Scene7)**

AEM as a Cloud Service 上的 Dynamic Media (Scene7) 没有为 HIPAA 做好准备，不能在启用了增强安全性的 AEM 环境中使用。

从 2025 年 4 月 AEM as a Cloud Service 发布开始，一项技术限制阻止了在启用了增强安全性的环境中配置 Dynamic Media (Scene7)。因此，**工具** > **云服务**&#x200B;中的&#x200B;**动态媒体配置**&#x200B;卡在这些环境中不再显示。

此外，使用 AEM 6.5 的客户应注意 Dynamic Media (Scene7) 堆栈没有为 HIPAA 做好准备。

### Dynamic Media Classic {#dynamic-media-classic}

**报告**

自 2025 年 4 月起，不再支持 Dynamic Media Classic 报告仪表板中的带宽选项卡。

请参阅[带宽和存储、报告类型](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。

## Assets 视图中的新增功能 {#new-features-assets-view}

**资产关系**

资产视图现在支持在简化的资产详细信息面板中查看和编辑资产关系。在内容中轻松添加来源和衍生等关系，以便用户可以更有效地找到相关的主要内容。

![资产关系示例](/help/assets/assets/asset-relations-example.png)

**比较资产的版本**

现在，您可以使用 Assets 视图快速选择资产的任何版本并将其与其最新版本进行比较。

![比较资产的版本](/help/assets/assets/version-compare2.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 预发行版功能

* [自适应Forms和表单片段的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：通用编辑器现在支持创建自适应Forms和可重用的表单片段。 作者能够以可视方式构建表单、配置提交操作和添加reCAPTCHA验证，所有这些都可以在简化的WYSIWYG创作环境中完成。 此功能可加快表单创建、增强一致性，并增强针对垃圾邮件和自动滥用的保护。

* [SharePoint 文档库 - 使用原始文件名保存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：现在，您可以选择使用表单附件的原始文件名将其保存在 SharePoint 文档库中。此增强功能简化了上传文件的识别和管理。

* **规则编辑器**：
   * [“When”子句中带有单击事件的二进制条件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：规则编辑器现在允许您在“When”子句中将按钮单击事件（_Is Clicked_）与其他条件相结合。这样就可以根据用户交互和其他因素更精确地控制规则的执行。注意：如果使用多个条件，单击事件必须是列出的第一个条件。
   * [字段和面板的验证条件](/help/forms/rule-editor-core-components-usecases.md)：规则编辑器现在包括 _IsValid_ 和 _IsNotValid_ 两个条件。这些条件允许您检查特定字段或整个面板（包括水平选项卡、垂直选项卡、可折叠项和向导等布局方法）的验证状态，从而根据验证结果改善表单导航和用户体验。
* [改进了 SharePoint 列表的范围管理](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint 网站现在支持所有管理路径，例如 /sites 和 /teams。这一增强功能有助于更加广泛地集成不同的 SharePoint 网站结构，为连接组织内容提供了更大的灵活性。
* [支持将记录文档保存到 SharePoint 列表](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：使用基于 SharePoint 列表的表单数据模型 (FDM) 创建的表单现在可以通过配置记录文档绑定引用字段属性将记录文档 (DoR) 保存到 SharePoint 列表。此增强功能可将受支持的表单数据和文档与 SharePoint 存储无缝集成。
* [自适应表单片段的自动映射支持](/help/forms/adaptive-form-fragments-core-components.md#auto-mapping-support-for-fragments-in-an-adaptive-form)：当架构对象与定义的片段结构对齐时，自适应Forms现在支持自动插入匹配片段，从而简化表单创建并促进重用。

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP) 与 Forms 集成

* [AEM Forms与Adobe Experience Platform的集成](/help/forms/aem-forms-aep-connector.md)： AEM Forms到Adobe Experience Platform的连接器实现了自适应Forms与Adobe Experience Platform之间的无缝集成。 此功能允许将表单数据映射到XDM架构并实时直接提交到AEP。 它简化了跨Adobe Experience Cloud解决方案的个性化和激活用例的数据捕获。

## CIF 加载项 {#cloud-services-cif}

### 增强功能 {#enhancements-cif}

* 为 CIF 产品引用数据类型添加产品变体选择
* **实验性**： PDP中CIF核心组件的[JSON+LD](/help/commerce-cloud/customizing/json-ld.md)
* **实验性**：[CIF清除缓存的能力](/help/commerce-cloud/configuring/clear-cache.md)

### 错误修复 {#bug-fixes-cif}

* 修复产品字段中的搜索问题
* 产品 URL 格式对于 #variant_sku 不按预期工作
* 无法向产品列表组件添加超过 20 个 SKU

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 基于 OpenAPI 的 API {#open-apis}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。需要身份验证的端点的凭据通过创建 Adobe Developer Console 项目生成，支持 OAuth 服务器到服务器、网页应用程序和单页面应用程序 (SPA)。

[请参阅](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)基于 OpenAPI 的 API[的完整列表了解详情](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)了解配置和使用方法。

观看此视频以了解如何配置经过身份验证的 API，以便以后使用：

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN 配置相关的增强功能 {#cdn-enhancements}

Adobe 管理的 CDN 提供灵活的配置选项，如这篇[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。以下是一些最新功能：

#### 在 CDN 日志中包含其他属性 {#props-in-cdnlogs}

这对于包括纠错调试和数据分析在内的场景很有用，您可以通过在[请求和响应变换](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)中设置 `logProperty` 操作，在 CDN 日志中包含超出默认属性的更多信息。

#### 区域、大洲和组织属性作为匹配条件 {#matching-conditions}

CDN 规则现在可以为包括阻止流量和重定向在内的用例根据区域、大洲和组织进行匹配。`clientRegion` 和 `clientContinent` 增强已受支持的 `clientCountry`，以基于地理位置进行匹配，`clientAsName` 和 `clientAsNumber` 则匹配自治系统，以识别大型 ISP、公司或云提供商。详细了解这些[新公开的请求属性](/help/security/traffic-filter-rules-including-waf.md#condition-structure)。

#### 设置 Cookie 值 {#cookie-attributes}

您可以在[响应变换](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations)中设置 cookie 属性。

### Java 21 支持 {#java21}

从 1 月份的版本开始，您可以使用 Java 21 和 Java 17 构建代码。您可以访问模式匹配、密封类和各种性能改进等新功能。有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 版本时，会自动部署性能更高的 Java 21 **运行时**。不过，Adobe 也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [ Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **运行时**&#x200B;已于 2 月份部署到您的开发/RDE 环境，它将于 **4 月 28 日和 29 日**&#x200B;应用于您的暂存/生产环境。请注意，使用 Java 21（或 Java 17）**构建代码**&#x200B;与 Java 21 运行时无关，因此您必须明确采取相应步骤来用 Java 21（或 Java 17）构建代码。

### 强制执行 AEM 的记录配置策略 {#logconfig-policy}

为了确保有效监控客户环境，AEM Java 日志必须保持一致的格式，并且不能被自定义配置覆盖。日志输出必须一直定向到默认文件。必须为 AEM 产品代码保留默认的日志级别。但是，可以为客户开发的代码调整日志级别。

为此，不得更改以下 OSGi 属性：
* **Apache Sling 日志配置**（PID：`org.apache.sling.commons.log.LogManager`）—*所有属性*
* **Apache Sling 日志记录器配置**（工厂 PID：`org.apache.sling.commons.log.LogManager.factory.config`）：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

5 月中旬，AEM 将强制实施一项政策，对这些属性所做的任何自定义更改都将被忽略。请检查并相应调整您的下游流程。例如，如果您使用日志转发功能：
* 如果您的日志记录目标需要一个自定义（非默认）日志格式，您可能需要更新您的摄取规则。
* 如果对日志级别的更改降低了日志的详细程度，请注意默认的日志级别可能会导致日志数量显著增加。

### AEM 日志转发至更多目标 - Beta 项目 {#log-forwarding-earlyadopter}

目前处于 Beta 阶段，您可以将 AEM 日志转发到 New Relic（使用 HTTPS）、Amazon S3 和 Sumo Logic。请注意，支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 (GA) AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。Adobe 希望了解您是否认为这项技术对 AEM Publish Delivery 和 Edge Delivery Services 项目有用。此外，请告诉我们您设想将其用于哪些用途，以便为产品路线图提供意见。

一些可能的用例：

* 使用 IdP 进行身份验证以控制内容访问权限
* 根据地理位置、设备类型、用户属性等呈现动态内容，从而进行个性化。
* 高级图像操作
* CDN 和来源之间的中间件
* 浏览器和第三方 API 之间的一层，可能用于重新格式化 API 响应
* 聚合多个来源的数据，使客户端浏览器更容易呈现它

请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

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
