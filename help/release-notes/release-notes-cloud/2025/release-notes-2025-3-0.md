---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.3.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.3.0 版的发行说明。'
feature: Release Information
role: Admin
exl-id: b9353092-88a0-477c-85f4-f916a4b8ba8f
source-git-commit: 81e5cfd699fee811fc2b072e3b65e9d463a338b2
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.3.0 版的发行说明 {#release-notes}

以下部分概述了 2025.3.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.3.0) 的发布日期为 2025 年 3 月 27 日。下一个功能版本 (2025.4.0) 计划于 2025 年 4 月 24 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看 2025 年 3 月发布概述视频，了解 2025.3.0 版本中的新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3463860?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 中的新增功能 {#new-features-dynamic-media}

**使用带有 Open API 的 Dynamic Media 投放的视频支持长格式**

带有 OpenAPI 的 Dynamic Media 现在支持长格式视频。长视频可支持最大 50GB，最长 2 小时。

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

自 2025 年 4 月起，不再支持 Dynamic Media Classic 报告仪表板中的带宽选项卡。

请参阅[带宽和存储、报告类型](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。


## Assets 视图中的新增功能 {#new-features-assets-view}


**支持根标记**

AEM Assets 现在支持将元数据表单内的标记属性映射到自定义元数据中。此外，作为管理员，您可以通过限制对特定根标记及其下标记的访问权限来限制用户对标记的可用性。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 自适应表单中的 HTML 电子邮件模板

自适应表单允许您使用 [HTML 电子邮件模板](/help/forms/html-email-templates-in-adaptive-forms.md)。HTML 电子邮件模板可让您在提交表单时发送内容丰富、个性化且具有视觉吸引力的电子邮件。这些电子邮件可使用表单数据进行自定义，并使用各种电子邮件标记（如图像和链接）进行增强。使用自适应表单，您可以上传包含 HTML 模板的文件，也可以使用纯文本编辑器来创建这些模板。

![HTML 电子邮件模板](/help/forms/assets/html-email.png)

#### 增强的云存储支持：将 PDF 直接上传至 Azure Blob 存储

AEM Forms 文档生成 API 现在可让您[直接将生成的 PDF 文档上传](/help/forms/early-access-ea-features.md#doc-generation-api)到 Azure Blob 存储。这种增强功能简化了存储和检索，提高了效率并与云工作流进行集成。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21 支持 {#java21}

从 1 月份的版本开始，您可以使用 Java 21 和 Java 17 构建代码。您可以访问模式匹配、密封类和各种性能改进等新功能。有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 版本时，会自动部署性能更高的 Java 21 **运行时**。不过，Adobe 也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [ Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **运行时**&#x200B;已于 2 月份部署到您的开发/RDE 环境，它将于 **4 月 28 日和 29 日**&#x200B;应用于您的暂存/生产环境。请注意，使用 Java 21（或 Java 17）**构建代码**&#x200B;与 Java 21 运行时无关，因此您必须明确采取相应步骤来用 Java 21（或 Java 17）构建代码。

### AEM 日志转发至更多目标 - Beta 项目 {#log-forwarding-earlyadopter}

目前处于 Beta 阶段，您可以将 AEM 日志转发到 New Relic（使用 HTTPS）、Amazon S3 和 Sumo Logic。请注意，支持 AEM 日志（包括 Apache/Dispatcher），但不支持 CDN 日志。发送电子邮件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，以获得访问权限。

虽然可以从 Cloud Manager 下载日志，但许多组织发现将这些日志流式传输到首选记录目标很有帮助。AEM 已经支持将 (GA) AEM 和 CDN 日志转发到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。此功能以自助方式配置，并使用配置管道进行部署。

更多信息请参阅[日志转发文档](/help/implementing/developing/introduction/log-forwarding.md)。

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。Adobe 希望了解您是否认为这项技术对 AEM Publish Delivery 和 Edge Delivery Services 项目有用。此外，请告诉我们您设想将其用于哪些用途，以便为产品路线图提供意见。

一些可能的用例：

* 使用 IdP 进行身份验证以控制内容访问权限
* 根据地理位置、设备类型、用户属性等呈现动态（个性化、本地化）内容。
* 高级图像操作
* CDN 和来源之间的中间件
* 浏览器和第三方 API 之间的一层，可能用于重新格式化 API 响应
* 聚合多个来源的数据，使客户端浏览器更容易呈现它

请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

### 基于 OpenAPI 的 API - 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。创建 Adobe Developer Console 项目时生成需要身份验证端点的凭据。

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。

* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites和Assets文件夹API
* [ Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎您的反馈，可以将意见通过电子邮件发送至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0)找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表。

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
