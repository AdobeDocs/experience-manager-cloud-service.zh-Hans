---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: fae92c9a41d866fd89ffb6fa10191fae4033037c
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 23%

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

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2024.5.0)为2024年5月30日。 下一个功能版本(2024.6.0)计划于2024年6月27日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看 2024 年 5 月发布概述视频，了解 2024.5.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Sites中的新增功能 {#sites-new-features}

**适用于 Edge Delivery Services 的 AEM 创作**

增强的稳定性和各种改进，以实现更好的创作体验。

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。

**内容片段控制台中的资产浏览功能**

内容作者现在可以浏览、查看图像和其他资产并对其执行操作，而无需离开内容片段控制台。

![资产浏览](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

是否有兴趣试用该功能并分享反馈？从您的官方电子邮件 ID 向 aemcs-headless-adopter@adobe.com 发送电子邮件即可详细了解早期采用者计划。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理视图中的新增功能 {#admin-view-new-features}

* WebM现在是处理视频配置文件时支持的输出文件。
* AEM in Express（导入和导出）的本机集成现在支持MP4。

### 资源视图中的新增功能 {#assets-view-new-features}

**将资源发布到AEM和Dynamic Media**

Experience Manager Assets现在使您能够快速 [将资源发布到Experience Manager和Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) 使用“资产”视图，而不切换到“管理员”视图。 您可以在上传、浏览和搜索资产时发布资产。

![检查发布状态1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms中的新增预发行功能 {#forms-new-prerelease-features}

#### 基于核心组件的自适应Forms的增强可视化规则编辑器

此版本对基于核心组件的自适应表单的可视化规则编辑器进行了重大升级。您现在可以：

* 在可视规则编辑器中创建规则以 [覆盖默认表单提交成功/失败消息](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* 在自适应Forms规则编辑器中，添加了 [为WHEN操作选择不同类型的字段](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* 表单作者现在可以将自定义函数应用于 [提交之前对数据进行预处理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* 使用 [**另存为草稿**](/help/forms/save-core-component-based-form-as-draft.md) 用于保存部分完成的表单以供以后提交的功能。 当用户需要中断填写表单并稍后返回表单时，这将很有用。



### AEM Forms中的早期采用者功能 {#forms-new-early-adopter-features}

AEM Forms早期采用者计划为您提供了一个独一无二的机会，让您能够比任何其他人更优先地访问前沿创新，并帮助塑造其发展。
项目提供了对多种创新的访问权限。

本发行说明列出了当前版本中提供的创新。 有关早期采用者计划下可用的创新的完整列表，请参阅 [AEM Forms早期采用者计划文档](/help/forms/early-adopter-ea-features.md).

#### 增强的机器人保护方法

AEM Forms通过添加对两个流行的CAPTCHA解决方案（Cloudflare Turnstile和hCaptcha）的支持，增强了其安全功能。 这进一步扩展了Google reCAPTCHA的可用功能，为用户在保护表单免受机器人和垃圾邮件提交影响方面提供了更多选择和灵活性。

* **Cloudflare Turnstile**：该无摩擦CAPTCHA通过不需要显式交互的简单挑战验证用户。 它可以无缝地集成到表单中，从而改善用户体验。
* **验证码**：这个注重隐私的验证码提供了用户友好的替代方案，重点关注数据隐私。 它旨在实现安全性和用户体验之间的平衡。
* **Google reCAPTCHA**： AEM Forms将继续支持reCAPTCHA v2和reCAPTCHA Enterprise，从而提供可靠且成熟的解决方案。

通过提供多个验证码选项，AEM Forms使您能够选择最符合您特定需求的解决方案。

是否准备好将任何CAPTCHA解决方案与您的自适应Forms集成？ 我们的文档提供了针对每种情况的详细说明： [Cloudflare Turnstile](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)， [验证码](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、和 [Google reCAPTCHA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### 表单服务

Forms服务为数据捕获生成交互式PDF forms。 它也可用于导入导出数据到现有交互式PDF表单或从其中导出数据，以及验证提交的数据。 以下是它的功能划分：

* **呈现Forms**：使用使用AEM Forms Designer创建的模板和（可选）XML数据生成交互式PDF表单。 这实际上会生成一个可填写的PDF表单，可以选择预填数据。
* **数据提取和导入**：将数据导入现有PDF表单，并从已填写的PDF表单中提取数据。 XDP和XML数据格式均受支持，导入到非XFAPDF forms（也称为AcroForms）时还支持FDF和XFDF数据。
* **数据验证**： ：根据使用AEM Forms Designer创建的模板，验证以XDP或XML格式提交的数据。

>[!IMPORTANT]
>
> 如果您有兴趣加入我们的早期采用者计划以进行任何早期采用者创新，只需将官方地址中的电子邮件发送至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 以请求访问权限。 您可以请求访问所有或任何特定的创新。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### OAuth服务器到服务器凭据支持AEM与其他Adobe解决方案的集成 {#S2S-OAuth-credentials}

Adobe Developer Console用于生成凭据以访问各种API。 其中一种凭据类型，服务帐户(JWT)凭据已弃用，推荐使用OAuth服务器到服务器凭据，AEM Cloud Service现在支持将其与其他Adobe解决方案(如Adobe Analytics和Adobe Target)集成。

[阅读有关弃用的信息](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) 和 [了解如何使用AEM创作UI](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 以配置与其他Adobe解决方案的集成。

### 源警报中的流量尖峰 {#traffic-spike-origin}

[接收主动通知](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) 通过操作中心，当原始流量模式显示DDoS攻击时，允许您调查和配置流量过滤规则。

### RDE的新功能 {#RDE-new-features}

[快速开发环境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 让开发人员在云中快速部署、审查和测试更改。 6月份将推出几项新功能。 此外，我们邀请您直接参与Adobe工程部的 [RDE不和谐通道](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### RDE支持使用站点主题和站点模板的前端代码 {#rde-frontend}

[RDE现在支持前端代码](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) 基于 [站点主题](/help/sites-cloud/administering/site-creation/site-themes.md) 和 [站点模板](/help/sites-cloud/administering/site-creation/site-templates.md)，适用于早期采用者。 对于RDE，这是使用命令行指令完成的，而不是 [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### 增强了RDE的日志记录 {#rde-logging}

在RDE中调试代码时，开发人员现在可以 [更有效地配置和流式传输日志](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)，且无需在版本控制中修改OSGI属性。 功能包括：

* 在每个包或类级别上声明日志级别
* 自定义日志输出格式
* 并行流式处理多个日志

#### RDE CLI增强功能 {#rde-cli-enhancements}

RDE命令行界面具有一些新功能，改善了开发人员体验：

* [setup命令是交互式的](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)，更便于在组织、项目和环境之间进行选择。 现在，也可以在命令行覆盖这些值。
* [安静模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) 以取得更少冗长的输出。
* [json模式](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) 用于以编程方式调用时的有用输出。

### 新的操作中心通知 {#actions-center-notifications}

[操作中心](/help/operations/actions-center.md) 会在发生重要事件时发送电子邮件通知，或者如果我们注意到您的代码或配置中发生了某些情况，那么您应该采取主动行动。 有三种新类型的通知：

* 通过高级网络基础架构的传出连接过多
* 使用已弃用的服务用户映射格式
* 潜在的DDoS攻击正在进行

### 早期采用者计划 {#foundation-early-adopter}

电子邮件 **<aemcs-cdn-config-adopter@adobe.com>**，指示您对以下哪些早期采用者计划感兴趣。

#### 使用自助API密钥清除CDN上的内容（早期采用者计划） {#purge-cdn}

以自助方式注册CDN清除API密钥，并使用它在CDN全局或一个或多个资源上使内容失效。 [了解详情](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 为客户管理的CDN (BYOCDN)自助创建X-AEM-Edge-Key（早期采用者计划） {#byocdn-keys}

以前，需要支持票证来生成配置客户管理的CDN所需的X-AEM-Edge-Key。 现在，可以通过使用配置管道部署的配置文件自助完成此操作，从而消除载入新环境的任何延迟。 [了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 客户端重定向（早期采用者项目） {#client-side-redirects-early-adopter}

在源代码控制中配置 301/302 客户端重定向，并部署到 CDN。[了解详情](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 请注意，还有其他一些与相关的功能可用 [CDN配置](/help/implementing/dispatcher/cdn-configuring-traffic.md)，包括请求和响应转换，以及将流量路由到非AEM站点。

#### 流量过滤规则警报（早期采用者计划） {#traffic-filter-rules-alerts-early-adopter}

最近发布的[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)包括可选择许可的 Web 应用程序防火墙 (WAF) 规则，可让您配置应允许或拒绝哪些流量。

加入率先采用者计划，以便在触发流量过滤器规则时向您发送警报。 当出现某些流量状况时，“操作中心”会通过发送电子邮件来通知您，以便采取适当的措施。

#### 商业用户可以在Git（早期采用计划）之外声明重定向 {#apache-rewritemaps-early-adopter}

与 AEM 6.5 类似，Apache/dispatcher 将会引入放置在发布存储库中特定位置的重写映射并对其进行加载，而无需执行 Web 层管道。这为企业用户提供了使用电子表格或UI（例如ACS Commons重定向映射管理器提供或作为客户应用程序的一部分创建的重定向功能）声明重定向的机会。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI)，用于加载动态内容（早期采用者计划） {#esi-early-adopter}

Adobe托管的CDN现在支持 [Edge Side Include (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，用于边缘级动态Web内容汇编的标记语言。 通过包含ESI片段，您可以在CDN上缓存具有较高TTL的整个HTML页面，同时更频繁地从源位置提取需要更高节奏更新（较低TTL）的较小部分。 <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

#### Real User Monitoring (RUM) Data Service（早期采用程序）

* **[Real Use Monitoring (RUM) Data Service现已正式提供](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** 为AEMas a Cloud Service启用客户端数据收集。
Real Use Monitoring服务（客户端集合）提供了交互的更精确反映，确保了对网站参与度的可靠衡量。 它使客户能够对其页面流量和性能进行高级分析。 这是详细了解页面性能并深入了解以改进该性能的绝佳机会。

## [!DNL Experience Manager] 指南 {#guides}

* **将主题或其元素发布到体验片段**
现在，Experience Manager指南允许您将主题或其元素发布到体验片段。 体验片段是一个模块化的内容单元，它集成了内容和布局。  体验片段非常有用，可以帮助您创建一致且引人入胜的体验。
* **能够将主题资源元数据传递到本机PDF输出**
您可以在生成本机PDF输出时添加主题资源元数据。 此功能可帮助您将不同主题（如主题标题和作者）的特定元数据添加到主题页眉和页脚。

有关版本中新增功能和增强功能及问题的更多信息，请查看 [Experience Manager指南发行路线图](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
