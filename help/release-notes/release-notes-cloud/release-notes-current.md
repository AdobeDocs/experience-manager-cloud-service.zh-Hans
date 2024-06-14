---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 68e2f6867a2cbcaf52fa6de259fe118e31ee7573
workflow-type: ht
source-wordcount: '1942'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.5.0) 的发布日期为 2024 年 5 月 30 日。下一个功能版本 (2024.6.0) 计划于 2024 年 6 月 27 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看 2024 年 5 月发布概述视频，了解 2024.5.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Sites 中的新增功能 {#sites-new-features}

#### AEM 翻译集成 {#translation-integration}

内容翻译操作和工作流现在可触发事件，以便从外部应用程序跟踪相关流程步骤和状态。正在生成下列事件。用户将能够使用 Adobe Developer Console 订阅事件。

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### 实际使用情况监控 (RUM) 数据服务 {#real-use-monitoring}

* **[真实用户监控 (RUM) 数据服务现已全面上线](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)**，可为 AEM as a Cloud Service 启用客户端数据收集功能。客户端收藏集的真实使用情况监控服务能够更准确地反映交互情况，确保可靠地衡量网站参与度。它使客户能够深入了解其页面流量和性能。这是深入了解您的页面性能并获取改进建议的绝佳机会。

#### 适用于 Edge Delivery Services 的 AEM 创作 {#edge-enhancements}

稳定性增强，多项改进带来更佳的创作体验。

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。

**内容片段控制台中的资源浏览功能**

内容作者现在可以浏览、查看图像和其他资源并对其执行操作，而无需离开内容片段控制台。

![资源浏览](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

是否有兴趣试用该功能并分享反馈？从您的官方电子邮件 ID 向 aemcs-headless-adopter@adobe.com 发送电子邮件即可详细了解早期采用者计划。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理视图中的新增功能 {#admin-view-new-features}

* WebM 现已成为视频处理配置文件中受支持的输出文件。
* Express 中的 AEM 原生集成现在支持 MP4（导入和导出）。

### Assets 视图中的新增功能 {#assets-view-new-features}

**发布资源到 AEM 和 Dynamic Media**

Experience Manager Assets 现在可让您使用“Assets”视图快速[将资源发布到 Experience Manager 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)，而无需切换到“管理员”视图。您可以在上传、浏览和搜索资源的同时发布资源。

![检查发布状态 1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms 预发行版中的新功能 {#forms-new-prerelease-features}

#### 针对核心组件自适应表单的增强型可视化规则编辑器

此版本对基于核心组件的自适应表单的可视化规则编辑器进行了重大升级。您现在可以：

* 在可视化规则编辑器中创建规则，以[覆盖默认表单提交成功/失败消息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers)。

* 在自适应表单规则编辑器中，添加了[为 WHEN 操作选择不同类型字段的功能](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)。

* 表单作者现在可以在提交前应用自定义函数[对数据进行预处理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)。

* 使用&#x200B;[**另存为草稿**](/help/forms/save-core-component-based-form-as-draft.md)&#x200B;功能保存部分填写的表单，以便稍后提交。当用户需要中断填写表单，稍后再回来继续填写时，此功能非常有用。



### AEM Forms 中的早期采用者功能 {#forms-new-early-adopter-features}

AEM Forms 早期采用者计划项目为您提供了一个独特的机会，让您能够抢先体验前沿创新，并帮助塑造其发展。
该计划支持多项创新。

本发行说明列出了当前版本中提供的创新功能。有关早期采用者计划下可用创新功能的完整列表，请参阅 [AEM Forms 早期采用者计划文档](/help/forms/early-adopter-ea-features.md)。

#### 增强的机器人防护方法

AEM Forms 通过增加对两种流行的验证码解决方案的支持，增强了其安全功能：Cloudflare Turnstile 和 hCaptcha。这为现有的 Google reCAPTCHA 增加了新的选择，为用户提供了更多的选择和灵活性，以保护他们的表单免受机器人和垃圾邮件的侵害。

* **Cloudflare Turnstile**：这种无摩擦的验证码通过简单的挑战来验证用户，无需明确的互动。它能够无缝集成到您的表单中，从而提升用户体验。
* **hCaptcha**：这款注重隐私的验证码提供了一种注重数据隐私的用户友好型替代方案。其旨在在安全性和用户体验之间取得平衡。
* **Google reCAPTCHA**：AEM Forms 继续支持 reCAPTCHA v2 和 reCAPTCHA Enterprise，提供可靠且完善的解决方案。

AEM Forms 提供多种验证码选项，您可以选择最适合您特定需求的解决方案。

您是否准备将这些验证码解决方案中的任意一个与您的自适应表单集成？我们的文档为每种验证码解决方案提供了详细的说明：[Cloudflare Turnstile](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)、[hCaptcha](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) 和 [Google reCAPTCHA](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components)。


### 表单服务

表单服务生成交互式 PDF 表单，用于数据捕获。它还可以用于将数据导入或导出到现有的交互式 PDF 表单，并验证提交的数据。以下是其功能的详细介绍：

* **渲染表单**：使用 AEM Forms Designer 创建的模板和可选的 XML 数据生成交互式 PDF 表单。这实际上会生成可填写的 PDF 表单，其中可选择预先填充数据。
* **数据提取和导入**：将数据导入现有 PDF 表单，也可从已填写的 PDF 表单中提取数据。支持 XDP 和 XML 数据格式，并且导入非 XFA PDF 表单（也称为 AcroForms）时还支持 FDF 和 XFDF 数据。
* **数据验证**：根据使用 AEM Forms Designer 创建的模板，验证 XDP 或 XML 格式的提交数据。

>[!IMPORTANT]
>
> 如果您有兴趣加入我们的早期采用者计划，了解任何早期采用者创新功能，只需从您的官方邮箱发送电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，申请访问权限即可。您可以申请访问全部或任何特定的创新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### OAuth 服务器到服务器凭据支持 AEM 与其他 Adobe 解决方案的集成 {#S2S-OAuth-credentials}

Adobe Developer Console 用于生成访问各种 API 的凭据。其中一种凭据类型是服务帐户 (JWT) 凭据，已被弃用，取而代之的是 OAuth 服务器到服务器凭据，AEM Cloud Service 现在支持与其他 Adobe 解决方案（例如 Adobe Analytics 和 Adobe Target）集成。

[阅读弃用信息](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)，并[了解如何使用 AEM 作者 UI](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)配置与其他 Adobe 解决方案的集成。

### 源流量尖峰警报 {#traffic-spike-origin}

当源站的流量模式表明存在 DDoS 攻击时，您可以通过操作中心[接收主动通知](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert)，以便调查并配置流量过滤规则。

### RDE 的新功能 {#RDE-new-features}

[快速开发环境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 让开发人员能够快速部署、审查和测试云中的变更。我们将在 6 月推出多项新功能。我们还邀请您直接在 [RDE Discord 频道](https://discord.com/channels/1131492224371277874/1245304281184079872)与 Adobe 工程团队交流。


#### RDE 支持使用网站主题和网站模板的前端代码 {#rde-frontend}

RDE 现在支持基于[网站主题](/help/sites-cloud/administering/site-creation/site-themes.md)和[网站模板](/help/sites-cloud/administering/site-creation/site-templates.md)的[前端代码](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde)，供早期采用者使用。在 RDE 的情况下，使用命令行指令而非[前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)实现这一点。

#### 增强的 RDE 日志记录功能 {#rde-logging}

在 RDE 中调试代码时，开发人员现在可以[使用命令行更高效地配置和传输日志](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)，而无需修改版本控制中的 OSGI 属性。功能包括：

* 在每个包或类级别上声明日志级别
* 自定义日志输出格式
* 并行传输多个日志

#### RDE CLI 增强功能 {#rde-cli-enhancements}

RDE 命令行界面新增了一些新功能，可以改善开发人员体验：

* [设置命令是交互式的](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)，使组织、程序和环境之间的选择变得更容易。现在也可以在命令行上覆盖这些值。
* [静音模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)，减少输出信息。
* [json 模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)，用于在程序调用时输出有用的信息。

### 新的操作中心通知 {#actions-center-notifications}

当发生重大事件时，或者当您的代码或配置出现异常时，[操作中心](/help/operations/actions-center.md)会发送电子邮件通知，提醒您采取主动操作。共有三种新的通知类型：

* 通过高级网络基础设施的传出连接过多
* 使用已弃用的服务用户映射格式
* 可能正在发生 DDoS 攻击

### 早期采用者计划 {#foundation-early-adopter}

发送电子邮件至 **<aemcs-cdn-config-adopter@adobe.com>**，表明您对以下哪些早期采用者计划感兴趣。

#### 使用自助式 API 密钥清除 CDN 上的内容（早期采用者计划） {#purge-cdn}

自助注册 CDN 清除 API 密钥，并使用该密钥对 CDN 上的内容进行全局或针对单个或多个资源的无效化操作。[了解详情](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 为客户管理的 CDN (BYOCDN) 自助创建 X-AEM-Edge-Key（早期采用者计划） {#byocdn-keys}

以前，需要提交支持请求工单才能生成配置客户托管 CDN 所需的 X-AEM-Edge-Key。现在，通过配置管道部署的配置文件，可以自助完成这项工作，从而消除了新环境导入过程中的任何延迟。[了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 客户端重定向（早期采用者项目） {#client-side-redirects-early-adopter}

在源代码控制中配置 301/302 客户端重定向，并部署到 CDN。[了解详情](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 请注意，目前已有与 [CDN 配置](/help/implementing/dispatcher/cdn-configuring-traffic.md)相关的其他多项功能可用，包括请求和响应变换以及将流量路由到非 AEM Sites。

#### 流量过滤规则警报（早期采用者计划） {#traffic-filter-rules-alerts-early-adopter}

最近发布的[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)包括可选择许可的 Web 应用程序防火墙 (WAF) 规则，可让您配置应允许或拒绝哪些流量。

加入早期采用者计划，这样当您的流量过滤规则触发时，您就可以收到警报。当出现某些流量状况时，“操作中心”会通过发送电子邮件来通知您，以便采取适当的措施。

#### 企业用户可以在 Git 之外声明重定向（早期采用者计划） {#apache-rewritemaps-early-adopter}

与 AEM 6.5 类似，Apache/dispatcher 将会引入放置在发布存储库中特定位置的重写映射并对其进行加载，而无需执行 Web 层管道。这为企业用户提供了使用电子表格或 UI 声明重定向的机会，例如 ACS Commons Redirect Map Manager 提供的重定向或作为客户应用程序的一部分创建的重定向。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI)，用于加载动态内容（早期采用者计划） {#esi-early-adopter}

Adobe Managed CDN 现在支持 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，这是一种用于边缘级动态 Web 内容组装的标记语言。通过加入 ESI 片段，您可以在具有更高 TTL 的 CDN 上缓存整个 HTML 页面，同时更频繁地从原始位置获取那些需要更高节奏更新（更低的 TTL）的较小部分。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guides {#guides}

* **将主题或其元素发布到体验片段中**
现在，Experience Manager Guides 允许您将主题或其元素发布到体验片段中。体验片段是一个集成内容和布局的模块化内容单元。体验片段非常有用，可以帮助您创建一致且引人入胜的体验。
* **能够将主题资源元数据传递给原生 PDF 输出**
您可以在生成原生 PDF 输出时添加主题资源元数据。此功能可帮助您将不同主题的特定元数据（如主题标题和作者）添加到主题页眉和页脚。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/cn/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## Experience Cloud 发行说明 {#experience-cloud}

您可以在[此处](https://experienceleague.adobe.com/cn/docs/release-notes/experience-cloud/current)找到有关其他 Experience Cloud 应用程序版本的信息。
要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。
