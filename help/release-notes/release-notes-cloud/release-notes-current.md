---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 8581ff75a68c045ccfbb6a525c1e08a6ee253d52
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 42%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2022 版或 2023 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2024.6.0)为2024年6月27日。 下一个功能版本(2024.7.0)计划于2024年7月25日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites中的新增功能 {#new-feature-sites}

**Real Use Monitoring (RUM)数据服务** {#real-use-monitoring}

实时监控(RUM)数据服务现已正式可用，可支持AEM as a Cloud Service的客户端数据收集。 此服务可更准确地反映用户交互，从而确保可靠地衡量网站参与度。 它为客户提供了有关其页面流量和性能的高级洞察，并提供了了解和提高页面性能的宝贵机会。

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。

**内容片段控制台中的资源浏览功能**

内容作者现在可以浏览、查看图像和其他资源并对其执行操作，而无需离开内容片段控制台。

![资源浏览](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

是否有兴趣试用该功能并分享反馈？从您的官方电子邮件 ID 向 aemcs-headless-adopter@adobe.com 发送电子邮件即可详细了解早期采用者计划。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Experience Manager Assets中的新增功能 {#new-features-assets}



**Content Hub**

Content Hub作为Experience Manager Assets as a Cloud Service的一部分提供，用于实现组织及其业务合作伙伴对品牌上内容的访问大众化。 借助Content Hub，您可以轻松查找和分发资源、重用和创建新的品牌内变体，以及大规模加快激活速度。

![Content Hub用户界面](/help/release-notes/assets/content-hub-ui.png)

**具有OpenAPI功能的Dynamic Media**

具有OpenAPI功能的Dynamic Media可跨Adobe和第三方应用程序扩展DAM，支持通过资产选择器或OpenAPI栈栈以任何渠道访问品牌认可的数字资产。 关键原则 — 无二进制副本，资产在边缘进行优化和转换以实现快速性能，提供公共或安全的资产。

![新的Dynamic Media数据流图](/help/assets/assets/dm-openapi-dfd.png)


### Assets 视图中的新增功能 {#assets-view-new-features}

**Assets Insights仪表板中提供了更多选项**

Assets Insights仪表板中现在提供了按资源类型和大小划分的资源计数。 这些选项可在您的Assets视图环境中提供实时数据。 它们按大小范围和资源类型详细列出资源的计数和百分比。

**更新了嵌入式Adobe Express编辑器**

* 与另存为新版本相比，改进了另存为新资产的用户体验。

* 以多页PDF和图像格式导出多页Express文档（以前仅支持单页）。 选择图像格式会将每个页面另存为DAM中的独特资产，以供下游分发。

* 支持在保存资产时在“保存”对话框中添加元数据。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms 中的新功能 {#forms-new-prerelease-features}

#### 针对核心组件自适应表单的增强型可视化规则编辑器

此版本显着升级了基于核心组件的自适应表单的可视规则编辑器。 您现在可以：

* 在可视规则编辑器中创建规则以 [覆盖默认表单提交成功/失败消息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* 在自适应表单规则编辑器中，添加了[为 WHEN 操作选择不同类型字段的功能](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)。

* 表单作者现在可以在提交前应用自定义函数[对数据进行预处理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)。

* 使用&#x200B;[**另存为草稿**](/help/forms/save-core-component-based-form-as-draft.md)&#x200B;功能保存部分填写的表单，以便稍后提交。当用户需要中断填写表单并稍后返回表单时，此功能非常有用。

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms抢先体验计划为您提供了一个独一无二的机会，让您能够抢在其他人之前独享尖端创新技术，并帮助塑造其发展形态。 该计划支持多项创新。

本发行说明列出了当前版本中提供的创新。 有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 增强的机器人防护方法

AEM Forms 通过增加对两种流行的验证码解决方案的支持，增强了其安全功能：Cloudflare Turnstile 和 hCaptcha。此功能是对现有Google reCAPTCHA的补充，为用户提供其他选项。 它增强了保护表单免受机器人和垃圾邮件提交影响的灵活性。

* **Cloudflare Turnstile**：该无摩擦CAPTCHA通过不需要显式交互的简单挑战验证用户。 它能够无缝集成到您的表单中，从而提升用户体验。
* **hCaptcha**：这款注重隐私的验证码提供了一种注重数据隐私的用户友好型替代方案。其旨在在安全性和用户体验之间取得平衡。
* **Google reCAPTCHA**：AEM Forms 继续支持 reCAPTCHA v2 和 reCAPTCHA Enterprise，提供可靠且完善的解决方案。

AEM Forms 提供多种验证码选项，您可以选择最适合您特定需求的解决方案。

是否准备好将任何这些CAPTCHA解决方案与您的自适应Forms集成？ Adobe文档提供了针对每种情况的详细说明： [Cloudflare Turnstile](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)， [验证码](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、和 [Google reCAPTCHA](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### 表单服务

表单服务生成交互式 PDF 表单，用于数据捕获。它还可以用于将数据导入或导出到现有的交互式 PDF 表单，并验证提交的数据。以下是其功能的详细介绍：

* **渲染表单**：使用 AEM Forms Designer 创建的模板和可选的 XML 数据生成交互式 PDF 表单。此功能会生成一个可填写的PDF表单，可以选择预填数据。
* **数据提取和导入**：将数据导入现有 PDF 表单，也可从已填写的 PDF 表单中提取数据。支持 XDP 和 XML 数据格式，并且导入非 XFA PDF 表单（也称为 AcroForms）时还支持 FDF 和 XFDF 数据。
* **数据验证**：根据使用 AEM Forms Designer 创建的模板，验证 XDP 或 XML 格式的提交数据。

>[!IMPORTANT]
>
> 如果您有兴趣加入Adobe的提前访问计划以进行任何提前访问创新，只需将官方地址中的电子邮件发送至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 以请求访问权限。 您可以申请访问全部或任何特定的创新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 与内容运行状况相关的操作中心通知早期采用者计划 {#actions-center-notifications}

[操作中心](/help/operations/actions-center.md) 当发生重要事件时，或者在注意到您的代码或配置存在某些问题时发送电子邮件通知，您应该采取主动行动。 Adobe现在引入了几种与内容运行状况相关的新类型通知。 此功能可通过早期采用者计划获取。 要参加测试，请联系Adobe客户关怀团队。

#### 页面包含大量节点 {#page-nodes}

大量的节点会降低渲染性能并减少页面加载时间。 在页面上检测到大量节点时，通过操作中心接收主动通知，这允许您采取必要步骤来减少页面中的节点总数。

#### 大量正在运行的工作流实例 {#running-workflows}

当创作环境中有大量正在运行的工作流时，工作流引擎性能会受到影响。 当检测到大量正在运行的工作流实例时，您将通过操作中心收到主动通知。 通过此流程，您可以配置清除作业以终止不必要的正在运行的工作流。

#### 直接添加到自定义组的用户 {#users-customgroups}

当用户直接添加到自定义组时，您会通过操作中心收到主动通知。 通过此过程可遵循IMS最佳实践，方法是将用户添加到相关的IMS组，然后包括这些IMS组作为AEM组的成员。

#### 缺少 JCR 内容 {#jcr-content}

检测到缺少JCR内容时，操作中心会主动通知您。 通过这种方法，您可以添加缺少的内容并防止某些AEM Assets功能出现故障。

#### 已完成的工作流未清除 {#workflows}

当超过90天的已完成工作流未被清除时，操作中心会主动通知您。 此方法有助于通过减少工作流实例的数量来提高工作流引擎的性能。

#### 缺少Sling资源 {#sling-resource}

在检测到缺少Sling资源时，操作中心会主动通知您。 此方法允许您添加缺少的资源并防止某些AEM Assets功能出现故障。

### 与内容交付相关的早期采用者计划 {#foundation-early-adopter}

发送电子邮件至 **<aemcs-cdn-config-adopter@adobe.com>**，表明您对以下哪些早期采用者计划感兴趣。

#### CDN的基本身份验证（早期采用者计划） {#basicauth-cdn}

Protect通过弹出基本身份验证对话框（需要用户名和密码）来识别某些内容资源。 此功能主要针对轻度身份验证用例（如审查内容的业务利益相关者），而不是作为最终用户访问权限的综合解决方案。 通过配置管道部署的Git中的配置文件管理中的用户名和密码列表，并引用机密类型的Cloud Manager环境变量。 [了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### 使用自助API密钥清除CDN上的内容（早期采用者计划） {#purge-cdn}

自助注册 CDN 清除 API 密钥，并使用该密钥对 CDN 上的内容进行全局或针对单个或多个资源的无效化操作。[了解详情](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 为客户管理的CDN (BYOCDN)自助创建X-AEM-Edge-Key（早期采用者计划） {#byocdn-keys}

以前，需要提交支持请求工单才能生成配置客户托管 CDN 所需的 X-AEM-Edge-Key。现在，可以通过使用配置管道部署的配置文件自助实现此结果，从而消除载入新环境的任何延迟。 [了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 客户端重定向（早期采用者计划） {#client-side-redirects-early-adopter}

在源代码控制中配置 301/302 客户端重定向，并部署到 CDN。[了解详情](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 请注意，目前已有与 [CDN 配置](/help/implementing/dispatcher/cdn-configuring-traffic.md)相关的其他多项功能可用，包括请求和响应变换以及将流量路由到非 AEM Sites。

#### 流量过滤规则警报（早期采用者计划） {#traffic-filter-rules-alerts-early-adopter}

最近发布的[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)包括可选择许可的 Web 应用程序防火墙 (WAF) 规则，可让您配置应允许或拒绝哪些流量。

加入早期采用者计划，这样当您的流量过滤规则触发时，您就可以收到警报。操作中心电子邮件通知可让您在发生某些流量情况时随时了解情况，以便采取适当措施。

#### 商业用户可以在Git（早期采用程序）之外声明重定向 {#apache-rewritemaps-early-adopter}

与AEM 6.5类似，Apache/Dispatcher摄取并加载放置在发布存储库中特定位置的重写映射，而无需执行Web层管道。 这种方法允许企业用户使用电子表格或UI（如ACS Commons重定向映射管理器或自定义应用程序）声明重定向。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI)，用于加载动态内容（早期采用者计划） {#esi-early-adopter}

Adobe Managed CDN 现在支持 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，这是一种用于边缘级动态 Web 内容组装的标记语言。通过加入 ESI 片段，您可以在具有更高 TTL 的 CDN 上缓存整个 HTML 页面，同时更频繁地从原始位置获取那些需要更高节奏更新（更低的 TTL）的较小部分。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guides {#guides}

您可以找到最新版本的Adobe Experience Manager Guides新增功能和增强功能的完整列表 [此处](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## Universal Editor {#universal-editor}

您可以找到通用编辑器版本的完整列表 [此处](/help/release-notes/universal-editor/current.md).

## 生成变体 {#generate-variations}

您可以查找生成变体版本的完整列表 [此处](/help/generative-ai/release-notes-generate-variations.md).

## Experience Cloud 发行说明 {#experience-cloud}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/release-notes/experience-cloud/current)找到有关其他 Experience Cloud 应用程序版本的信息。
要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。