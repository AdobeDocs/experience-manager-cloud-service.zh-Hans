---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.2.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2025.2.0 版的发行说明。'
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: 403ffbede5438131d0b0e770215b990e2d16c018
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.2.0 版的发行说明 {#release-notes}

以下部分概述了 2025.2.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2023 版或 2024 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.2.0) 的发布日期为 2025 年 3 月 4 日。下一个功能版本 (2025.3.0) 计划于 2025 年 3 月 27 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2025 年 2 月版概述视频，大致了解 2025.2.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites 中的新增功能 {#new-features-sites}

**内容片段自动标记**

创建内容片段时，现在可以自动继承分配给内容模型的标记。这样可以对存储在内容片段中的内容进行强大的自动分类。

**内容片段 UUID 支持**

内容片段 UUID 支持现在是 GA。新功能不会改变 AEM 中基于路径的运行行为，例如移动、重命名、转出，因为路径会自动调整，但它可以使内容片段的外部使用更容易、更稳定，尤其是在使用 GraphQL 查询时，该查询通过 ByPath 查询直接针对单个片段。如果片段路径发生变化，此类查询可能会中断。现在使用新的 ById 查询类型时，查询保持稳定，因为在路径发生变化的情况下片段的 UUID 不会改变。

**内容片段编辑器和 GraphQL 中支持具有 OpenAPI 功能的动态媒体**

不是存储在内容片段中，而是存储在不同的 AEM as a Cloud Service 计划中，并且启用了具有 OpenAPI 功能的新动态媒体的资产，现在可以在内容片段中使用。新内容片段编辑器中的图像选择器现在允许选择“远程”存储库作为片段中引用的图像资产的来源。并且，在使用 AEM GraphQL 投放此类内容片段时，JSON 响应现在包含远程资产 (assetId、repositoryId) 所需的属性，这样客户端应用程序可以创建相应的具有 OpenAPI 功能的动态媒体 URL 来获取图像。

**内容片段编辑器推出**

我们将继续使用[Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md)（使用频谱UI）在AEM as a Cloud Service中启用新的[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)。 它已在 2024 年 11 月成为所有 Cloud Service 开发者环境的默认设置，2025 年 4 月 1 日将成为所有暂存环境的默认设置，并将在 2025 年 5 月 1 日成为所有生产环境的默认设置。在所有情况下，用户仍然可以选择恢复到 AEM Touch UI 中传统的内容片段编辑器。

**翻译 HTTP API**

AEM Translation HTTP REST API 有一段时间是早期采用者模式，现在是 GA。文档可在[此处找到。](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/translation/) API允许自动执行AEM中内容的翻译管理流程中所需的步骤。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新增功能 {#new-features-assets}

**动态媒体新包装结构**

现在提供一种更新的动态媒体包装结构，以更好地符合市场预期并支持跟踪。新的包装结构包括：

* Dynamic Media Prime，包括具有 OpenAPI 功能和视频的动态媒体，以增强投放。

* Dynamic Media Ultimate 增加了投放和转换功能，以满足更高的使用要求。

您必须有 Assets as a Cloud Service Prime 或 Ultimate 才能使用新的包装结构。

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的字幕来提高视频的可观看性，并增强用户体验。字幕是根据原始音频、任何附加音轨生成的，或者视频属性页面“字幕和音频”选项卡中提供额外字幕。支持超过 60 种语言，可以在发布视频之前查看和预览字幕。

**自定义搜索过滤器**

自定义搜索过滤器提高了查找相关信息的准确度和效率。它允许进行更加定制的搜索，根据品牌、产品、类别或其他关键标识符等特定属性筛选数据。这可以改善组织，减少仔细检查不相关结果所花费的时间，并能够更快地做出决策。它还支持可扩展性，因为大型数据集会更易于导航和分析。

![自定义搜索过滤器](/help/assets/assets/custom-search-filters.png)

### Content Hub 中的早期访问功能 {#early-access-content-hub}

除了现有的静态演绎版之外，Content Hub 现在还允许您查看和下载动态及智能裁切演绎版。作为 Content Hub 管理员，您还可以使用配置用户界面配置这些演绎版对于用户的可用性。

![动态演绎](/help/assets/assets/download-single-asset-renditions-dynamic.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 自适应表单中的 HTML 电子邮件模板

自适应表单允许您使用 [HTML 电子邮件模板](/help/forms/html-email-templates-in-adaptive-forms.md)。HTML 电子邮件模板可让您在提交表单时发送内容丰富、个性化且具有视觉吸引力的电子邮件。这些电子邮件可使用表单数据进行自定义，并使用各种电子邮件标记（如图像和链接）进行增强。使用自适应表单，您可以上传包含 HTML 模板的文件，也可以使用纯文本编辑器来创建这些模板。

![HTML 电子邮件模板](/help/forms/assets/html-email.png)

#### 增强的云存储支持：将 PDF 直接上传至 Azure Blob 存储

AEM Forms 文档生成 API 现在允许您[直接将生成的 PDF 文档上传](/help/forms/early-access-ea-features.md#doc-generation-api)到 Azure Blob 存储。这种增强功能简化了存储和检索，提高了效率并与云工作流进行集成。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21 支持 {#java21}

正如在一月份的发行说明中提到的，您现在可以使用 Java 21 构建代码，其中包括新功能（如切换语句的模式匹配、密封类）和性能改进。Java 17 版本也获得了新的支持。有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 构建时，将自动部署性能更高的 Java 21 **运行时**。不过，我们也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [&#x200B; Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> 2 月份，Java 21 **运行时**&#x200B;被部署到 dev/RDE 环境（已使用 Java 17 或 21 构建的环境除外，这些环境已经有 Java 21 运行时）。Java 21 将于 4 月应用于暂存/生产环境。

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

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。

* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites和Assets文件夹API
* [&#x200B; Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

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
