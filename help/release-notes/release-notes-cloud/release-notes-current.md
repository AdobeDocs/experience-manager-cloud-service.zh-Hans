---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 11d019e10dc9246e5560f7fe27472d047cdc7caa
workflow-type: tm+mt
source-wordcount: '1551'
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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.4.0)的发布日期是2025年4月24日。 下一个功能版本(2025.5.0)计划于2025年5月29日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites中的新增功能 {#enhancements-sites}

**新的内容片段模型管理员UI**

在处理AEM内容片段时，进一步填写新客户端用户界面的列表，新的管理员UI现在可用于内容片段模型。 新UI提供了一个简洁的现代列表视图，该视图允许使用过滤器搜索模型，并显示模型标记以及基于特定模型存在哪些内容片段。 文档可在[此处](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)找到。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

增强的安全环境中不支持&#x200B;**Dynamic Media (Scene7)**

AEM as a Cloud Service上的Dynamic Media (Scene7)不符合HIPAA要求，并且无法在启用了增强安全性的AEM环境中使用。

从2025年4月版AEM as a Cloud Service开始，技术限制会阻止在具有增强安全性的环境中配置Dynamic Media (Scene7)。 因此，**工具** > **云服务**&#x200B;下的&#x200B;**Dynamic Media配置**&#x200B;卡在这些环境中不再可见。

此外，使用AEM 6.5的客户应该知道Dynamic Media (Scene7)栈栈未就绪，无法用于HIPAA。

### Dynamic Media Classic {#dynamic-media-classic}

**报表**

自 2025 年 4 月起，不再支持 Dynamic Media Classic 报告仪表板中的带宽选项卡。

请参阅[带宽和存储、报告类型](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。


## Assets视图中的新增功能 {#new-features-assets-view}

**资产关系**

资产视图现在支持在简化的资产详细信息面板中查看和编辑资产关系。轻松地将Source和派生等关系添加到内容，以便用户可以更有效地查找相关主页内容。

![Assets关系示例](/help/assets/assets/asset-relations-example.png)

**比较资源的版本**

您现在可以使用Assets视图快速选择资源的任何版本并将其与其最新版本进行比较。

![比较资源的版本](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 预发行版功能

* [通用编辑器 — 表单片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：通用编辑器现在允许您为自适应Forms创建和重用表单片段。 这些片段是可重用的表单部分（例如，联系人详细信息、同意字段），可以一次构建并应用于多个表单。 此功能可简化表单创建、确保一致性并提高创作效率。

* [SharePoint文档库 — 使用原始文件名保存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：现在，您可以选择在将表单附件存储在SharePoint文档库中时，使用原始文件名保存表单附件。 此增强功能简化了已上传文件的识别和管理。

* **规则编辑器**：
   * “When”子句中带有Click事件的[Binary条件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：规则编辑器现在允许将按钮点击事件(_Is Clicked_)与“When”子句中的其他条件组合。 这样可根据用户交互和其他因素更精确地控制规则执行。 注意：使用多个条件时，click事件必须是列出的第一个条件。
   * [字段和面板的验证条件](/help/forms/rule-editor-core-components-usecases.md)：规则编辑器现在包含&#x200B;_IsValid_&#x200B;和&#x200B;_IsNotValid_&#x200B;条件。 利用这些功能，可检查特定字段或整个面板（包括水平选项卡、垂直选项卡、折叠项和向导等布局）的验证状态，从而促进基于验证结果的表单导航和用户体验的改进。
* **已改进SharePoint列表的范围管理**： SharePoint站点现在支持所有托管路径，例如/sites和/teams。 此增强功能支持跨各种SharePoint站点结构进行更广泛的集成，在连接到组织内容方面提供了更大的灵活性。
* **支持将记录文档保存到SharePoint列表**：通过配置记录文档绑定引用字段属性，使用基于SharePoint列表的表单数据模型(FDM)创建的Forms现在可以将记录文档(DoR)保存到SharePoint列表。 此增强功能支持将支持的表单数据和文档与SharePoint存储无缝集成。

### AEM Forms中的抢先体验功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP)与Forms的集成

Forms与AEP之间的集成功能现已可供早期采用者使用。

## CIF 加载项 {#cloud-services-cif}

### 增强功能 {#enhancements-cif}

* 为CIF产品引用数据类型添加产品变型选择
* [实验性]：PDP中CIF核心组件的JSON+LD
* [实验性]： CIF清除缓存的功能

### 错误修复 {#bug-fixes-cif}

* 修复产品字段中的搜索问题
* 产品URL格式无法按预期用于#variant_sku
* 无法向产品列表组件添加超过20个SKU

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 基于OpenAPI的API {#open-apis}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。需要身份验证的端点的凭据通过创建Adobe Developer Console项目生成，并支持OAuth服务器到服务器、Web应用程序和单页应用程序(SPA)。

[查看基于OpenAPI的API的完整列表](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)，[了解更多](/help/implementing/developing/open-api-based-apis.md)，并尝试使用说明配置和使用情况的[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)。

观看此视频，了解如何配置经过身份验证的API以供将来使用：

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN配置相关的增强功能 {#cdn-enhancements}

Adobe-Managed CDN提供了灵活的配置选项，如[配置管道文章](/help/operations/config-pipeline.md#configurations)中所述。 以下是一些近期的功能：

#### 在CDN日志中包含其他属性 {#props-in-cdnlogs}

对于包括调试和数据分析在内的场景，通过在[请求和响应转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)中设置`logProperty`操作，您可以在CDN日志中包含超出默认属性的更多信息。

#### 区域、大陆和组织属性作为匹配条件 {#matching-conditions}

CDN规则现在可以根据地区、大陆和组织的用例进行匹配，包括阻止流量和重定向。 `clientRegion`和`clientContinent`将已支持的`clientCountry`扩充为基于地理位置进行匹配，而`clientAsName`和`clientAsNumber`将匹配自治系统以识别大型ISP、公司或云提供商。 了解有关这些[新公开的请求属性](/help/security/traffic-filter-rules-including-waf.md#condition-structure)的更多信息。

#### 设置Cookie值 {#cookie-attributes}

您可以在[响应转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations)中设置Cookie属性。

### Java 21支持 {#java21}

从 1 月份的版本开始，您可以使用 Java 21 和 Java 17 构建代码。您可以访问模式匹配、密封类和各种性能改进等新功能。有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 版本时，会自动部署性能更高的 Java 21 **运行时**。不过，Adobe 也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [ Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **运行时**&#x200B;已于 2 月份部署到您的开发/RDE 环境，它将于 **4 月 28 日和 29 日**&#x200B;应用于您的暂存/生产环境。请注意，使用 Java 21（或 Java 17）**构建代码**&#x200B;与 Java 21 运行时无关，因此您必须明确采取相应步骤来用 Java 21（或 Java 17）构建代码。

### AEM日志转发到更多目标 — Beta计划 {#log-forwarding-earlyadopter}

目前处于 Beta 阶段，您可以将 AEM 日志转发到 New Relic（使用 HTTPS）、Amazon S3 和 Sumo Logic。请注意，支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 (GA) AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。Adobe 希望了解您是否认为这项技术对 AEM Publish Delivery 和 Edge Delivery Services 项目有用。此外，请告诉我们您设想将其用于哪些用途，以便为产品路线图提供意见。

一些可能的用例：

* 使用 IdP 进行身份验证以控制内容访问权限
* Personalization ：根据地理位置、设备类型、用户属性等呈现动态内容。
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
