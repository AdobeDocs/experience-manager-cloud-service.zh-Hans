---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: edfec41a9e33fbe818cb19f878ac42d435d62419
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 47%

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

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前功能版本(2025.2.0)的发布日期是2025年3月4日。 下一个功能版本(2025.3.0)计划于2025年3月27日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### AEM Sites中的新增功能 {#new-features-sites}

**内容片段自动标记**

现在，在创建内容片段时，可以自动继承分配给内容模型的标记。 这允许对内容片段中存储的内容进行强大的自动分类。

**内容片段UUID支持**

内容片段UUID支持现在为GA。 新功能不会改变AEM中基于路径的操作行为（例如移动、重命名、转出，这些操作会自动调整路径），但它可以让内容片段的外部使用更容易、更稳定，尤其是在使用GraphQL查询（通过ByPath查询直接针对单个片段）时。 如果片段路径发生更改，此类查询可能会中断。 使用新的ById查询类型时，查询现在保持稳定，因为路径这样做时，片段的UUID不会更改。

内容片段编辑器和GraphQL中支持OpenAPI的** Dynamic Media **

与内容片段不同，Assets存储在AEM as a Cloud Service程序中，并通过新的Dynamic Media （具有OpenAPI功能）启用，现在可以在内容片段中使用。 现在，新内容片段编辑器中的图像选择器允许选择“远程”存储库作为片段中要引用的图像资产的源。 在使用AEM GraphQL交付此类内容片段时，JSON响应现在包含远程资产(assetId、repositoryId)所需的属性，以便客户端应用程序可以创建具有OpenAPI URL的相应Dynamic Media来获取图像。

**翻译HTTP API **

已处于早期采用者模式一段时间的AEM翻译HTTP REST API现在已正式推出。 文档可在[此处](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/)找到。 利用API，可自动执行AEM中内容的翻译管理流程中所需的步骤。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新增功能 {#new-features-assets}

**Dynamic Media新打包结构**

现在提供了更新的Dynamic Media打包结构，以便更好地符合市场预期并支持跟踪。 新的封装结构包括：

* Dynamic Media Prime，其中包括使用OpenAPI和视频增强交付的Dynamic Media。

* Dynamic Media Ultimate添加了交付和转换功能，以满足更苛刻的使用要求。

您必须拥有Assets as a Cloud Service Prime或Ultimate才能从新的打包结构中受益。

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在提供准确的字幕，从而提高辅助功能并增强用户体验。 字幕由原始音频生成，任何附加的音频曲目或额外的字幕在视频属性页面的“字幕和音频”选项卡中提供。 支持超过 60 种语言，可以在发布视频之前查看和预览字幕。

**自定义搜索筛选器**

自定义搜索筛选器可提高查找相关信息的精度和效率。 它允许进行更定制的搜索，根据特定属性（如品牌、产品、类别或其他关键标识符）过滤数据。 这可以改善组织结构，减少花在筛选无关结果上的时间，并实现更快的决策。 它还支持可扩展性，因为大型数据集变得更加易于导航和分析。

![自定义搜索筛选器](/help/assets/assets/custom-search-filters.png)


### Content Hub中的抢先体验功能 {#early-access-content-hub}

除了现有的静态演绎版之外，Content Hub现在还允许您查看和下载动态和智能裁剪演绎版。 作为Content Hub管理员，您还可以使用配置用户界面配置这些演绎版的可用性。

![动态演绎](/help/assets/assets/download-single-asset-renditions-dynamic.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 自适应Forms中的HTML电子邮件模板

自适应Forms允许您使用[HTML电子邮件模板](/help/forms/html-email-templates-in-adaptive-forms.md)。 HTML 电子邮件模板可让您在提交表单时发送内容丰富、个性化且具有视觉吸引力的电子邮件。这些电子邮件可使用表单数据进行自定义，并使用各种电子邮件标记（如图像和链接）进行增强。使用自适应表单，您可以上传包含 HTML 模板的文件，也可以使用纯文本编辑器来创建这些模板。

![HTML 电子邮件模板](/help/forms/assets/html-email.png)

#### 增强的云存储支持：将 PDF 直接上传至 Azure Blob 存储

AEM Forms Document Generation API现在允许您[直接将生成的PDF文档](/help/forms/early-access-ea-features.md#doc-generation-api)上传到Azure Blob Storage。 这种增强功能简化了存储和检索，提高了效率并与云工作流进行集成。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21 支持 {#java21}

如1月发行说明中所述，您现在可以使用Java 21构建代码，其中包括新增功能（例如，交换语句的模式匹配、密封类）和性能改进；此外，还新支持Java 17构建。 有关配置步骤（包括更新 Maven 项目和库版本），请参阅文章[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)。

当检测到 Java 17 或 21 构建时，将自动部署性能更高的 Java 21 **运行时**。不过，我们也建议使用 Java 11 构建的环境选择 Java 21 运行时，具体方法是发送电子邮件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [ Java 21 运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> 2月，将Java 21 **运行时**&#x200B;部署到开发/RDE环境（除了已使用Java 17或21构建的环境，这些环境已具有Java 21运行时）。 Java 21将于4月应用于暂存/生产环境。

### Edge 计算 - 请求反馈！ {#edge-computing-feedback}

Edge 计算使数据处理更接近浏览器，其好处包括减少延迟。Adobe希望了解您是否发现这项技术对AEM Publish Delivery和Edge Delivery Services项目很有用。 此外，请告知我们您打算将它用作产品路线图的输入内容。

一些可能的用例：
* 使用IdP进行身份验证以授予对内容的访问权限
* 根据地理位置、设备类型、用户属性等呈现动态（个性化、本地化）内容。
* 高级图像操作
* CDN和源之间的中间件
* 浏览器和第三方API之间的层，可能会重新设置API响应的格式
* 聚合来自多个源的数据，使客户端浏览器更容易呈现

请发送电子邮件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，欢迎提问并发表评论！

### 基于 OpenAPI 的 API - 早期采用者计划 {#open-apis-earlyadopter}

开发人员可以将 AEM as Cloud Service 功能深度集成到他们自己的应用程序和工具中。新的 AEM as a Cloud Service API 遵循 OpenAPI 规范，目标是保持一致、记录良好且用户友好。创建 Adobe Developer Console 项目时生成需要身份验证端点的凭据。

详细了解[基于 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md)，并尝试[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)说明配置和使用方法。

具体来说，下面列出的 API 端点可作为早期采用者计划的一部分使用。如果有兴趣，请发邮件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，描述您打算如何使用它们。

* [Sites 内容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [资产 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和资产文件夹 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [ Forms 通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎您的反馈，可以将意见通过电子邮件发送至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表。

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
