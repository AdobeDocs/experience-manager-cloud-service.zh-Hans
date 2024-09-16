---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.7.0 版的发行说明。'
feature: Release Information
role: Admin
exl-id: 6194df9d-8c3c-4c7f-be59-099b970a565a
source-git-commit: 79bf9d669c1b8757f456b83aad87550df306c78b
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 76%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.7.0 版的发行说明 {#release-notes}

以下部分概述了 2024.7.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2022 版或 2023 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.7.0) 的发布日期为 2024 年 7 月 25 日。下一个功能版本 (2024.8.0) 计划于 2024 年 8 月 29 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请观看 2024 年 7 月发布概述视频，大致了解 2024.7.0 版本中的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#new-feature-sites}

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。

**内容片段控制台中的资源浏览功能**

内容作者现在可以浏览、查看图像和其他资源并对其执行操作，而无需离开内容片段控制台。

![资源浏览](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

是否有兴趣试用该功能并分享反馈？从您的官方电子邮件 ID 向 aemcs-headless-adopter@adobe.com 发送电子邮件即可详细了解早期采用者计划。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**使用资产选择器上传资产**

资产选择器现在为内容作者提供了直接从选择器上传最终资产的功能，既可以拖动也可以从本地文件系统浏览。 此功能允许从您选择的应用程序将最终资产上传到DAM。

### Dynamic Media中的抢先访问功能 {#dm-early-access}

**AI生成的视频字幕**

AdobeDynamic Media中人工智能生成的视频字幕，使用人工智能为视频内容自动生成字幕。 此功能旨在通过提供准确的实时字幕来提高辅助功能并增强用户体验。 人工智能分析视频的音轨以转录语音并创建字幕，这些可以编辑以便精确或定制。 这些字幕有助于满足辅助功能要求，并提升依赖或偏好基于文本的视频支持的受众的视频参与度。

若要提前访问您Dynamic Media帐户上由AI生成的字幕支持，请[创建并提交Adobe的客户支持案例](/help/assets/dynamic-media/video.md##enable-dash)。

### Assets 视图中的新增功能 {#assets-view-new-features}

**Content Credentials 集成**

Experience Manager Assets 现在支持指定图像格式的 Content Credentials。此功能提供了有关资产的族系以及创建资产的方式（包括是否使用GenAI修改了资产）的信息。

![Content Credentials](/help/assets/assets/content-credentials.png)

**文件夹内容的视觉预览**

现在，在浏览或搜索内容时，Experience Manager Assets会在文件夹缩略图上显示文件夹内容的可视预览，这改进了AEM Assets存储库中可用资源的可发现性。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 中的新功能 {#forms-new-prerelease-features}

#### 针对核心组件自适应表单的增强型可视化规则编辑器

自适应表单作者可以使用可重复的表单字段和现成的可视化规则编辑器功能，在表单中创建复杂的业务逻辑，而无需开发团队进行自定义或提供支持。

### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以先于其他人独家访问尖端创新，并帮助塑造其发展。该计划支持多项创新。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### 使用通用编辑器创作自适应表单

利用 Adobe Experience Manager [通用编辑器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) 通过所见即所得的拖放创作功能创建自适应表单，实现无头和有头注册体验，并通过 Edge Delivery Service 交付。自适应表单作者可以轻松地为网页中的表单变体创建和启动实验。 此功能使他们能够为最终用户确定最佳性能体验。

>[!IMPORTANT]
>
> 如果您有兴趣加入 Adobe 的 Early Access Program，了解任何早期访问创新功能，只需从您的官方邮箱发送电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，申请访问权限即可。您可以申请访问全部或任何特定的创新。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 使用自助式 API 密钥清除 CDN 上的内容 {#purge-cdn}

使用 HTTP Cache-Control 标头设置 TTL 是平衡内容传递性能和内容新鲜度的有效方法。但是，在必须立即提供更新内容的情况下，直接清除CDN缓存可能会有帮助。

[了解如何](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)使用Cloud Manager配置管道自助提供清除API令牌的配置，以使您可以[调用清除API](/help/implementing/dispatcher/cdn-cache-purge.md)，并使用以下任一变体：

* 单一 URL
* 使用标签的多个 URL
* 全面清除 CDN 缓存

### 为客户管理的 CDN 自助配置 X-AEM-Edge-Key {#customermanaged-keys}

以前，需要提交支持请求工单才能生成配置客户托管 CDN 所需的 X-AEM-Edge-Key。此工作流现在通过声明使用配置管道部署的配置文件中的键值来提供自助服务，从而消除载入新环境的任何延迟。 [了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

### 流量筛选规则警报 {#traffic-filter-rules-alerts}

流量过滤器规则包括可选许可的Web应用程序防火墙(WAF)规则，允许您配置应该阻止哪些流量。

现在，只要触发流量过滤器规则，您就可以[订阅警报](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts)。 当出现某些流量状况时，“操作中心”会通过发送电子邮件来通知您，以便采取适当的措施。

### 内容投放相关的早期采用者计划 {#foundation-early-adopter}

发送电子邮件至 **<aemcs-cdn-config-adopter@adobe.com>**，表明您对以下哪些早期采用者计划感兴趣。

#### CDN 上的基本身份验证（早期采用者计划） {#basicauth-cdn}

通过弹出需要用户名和密码的基本身份验证对话框来保护某些内容资源。此功能主要针对轻度身份验证用例，例如业务利益相关者审查内容，而不是作为最终用户访问权限的综合解决方案。用户名和密码列表通过 git 中的配置文件进行管理，该文件通过配置管道部署，并引用秘密类型的 Cloud Manager 环境变量。[了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### 客户端重定向（早期采用者项目） {#client-side-redirects-early-adopter}

在源代码控制中配置 301/302 客户端重定向，并部署到 CDN。[了解详情](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> 请注意，目前已有与 [CDN 配置](/help/implementing/dispatcher/cdn-configuring-traffic.md)相关的其他多项功能可用，包括请求和响应变换以及将流量路由到非 AEM Sites。

#### 企业用户可以在 Git 之外声明重定向（早期采用者计划） {#apache-rewritemaps-early-adopter}

与 AEM 6.5 类似，Apache/dispatcher 会引入放置在发布存储库中特定位置的重写映射并对其进行加载，而无需执行 Web 层管道。这种方法让业务用户使用电子表格或 UI（如 ACS Commons Redirect Map Manager 或自定义应用程序）声明重定向<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->。

#### Edge Side Includes (ESI)，用于加载动态内容（早期采用者计划） {#esi-early-adopter}

Adobe Managed CDN 现在支持 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，这是一种用于边缘级动态 Web 内容组装的标记语言。通过加入 ESI 片段，您可以在具有更高 TTL 的 CDN 上缓存整个 HTML 页面，同时更频繁地从原始位置获取那些需要更高节奏更新（更低的 TTL）的较小部分。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### 内容健康相关行动中心通知早期采用者计划 {#actions-center-notifications}

当发生重要事件时，或者当您发现有关您的代码或配置的某些情况而需要您采取主动行动时，[Actions Center](/help/operations/actions-center.md)会发送电子邮件通知。Adobe 现在推出了几种与您的内容健康状况相关的新类型的通知。此功能可通过早期采用者计划获得。如需参与，请联系 Adobe 客户服务。

#### 页面包含大量节点 {#page-nodes}

大量节点会降低渲染性能并减少页面加载时间。当在页面上检测到大量节点时，通过操作中心接收主动通知，允许您采取必要的步骤来减少页面内的总节点数。

#### 大量正在运行的工作流实例数 {#running-workflows}

当创作环境中正在运行大量工作流时，工作流引擎的性能会受到影响。当检测到大量正在运行的工作流实例时，您会通过操作中心收到主动通知。此过程允许您配置清除作业以终止不必要的正在运行的工作流。

#### 直接添加到自定义组的用户 {#users-customgroups}

当用户被直接添加到自定义组时，您会通过操作中心收到主动通知。此过程允许您遵循 IMS 最佳实践，将用户添加到相关的 IMS 组，然后将这些 IMS 组作为 AEM 组的成员包括在内。

#### 缺少 JCR 内容 {#jcr-content}

当检测到缺少的 JCR 内容时，操作中心会主动通知您。通过这种方法，您可以添加缺失的内容并防止某些 AEM Assets 功能失败。

#### 未清除已完成的工作流 {#workflows}

当超过 90 天的已完成工作流程尚未清除时，操作中心会主动通知您。这种方法有助于减少工作流实例的数量，从而提高工作流引擎的性能。

#### 缺少 Sling 资源 {#sling-resource}

当检测到缺少 Sling 资源时，操作中心会主动通知您。通过这种方法，您可以添加缺失的资源并防止某些 AEM Assets 功能失败。

## [!DNL Experience Manager] Guides {#guides}

您可以找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表 [这里](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0)。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## Universal Editor {#universal-editor}

您可以在[此处](/help/release-notes/universal-editor/current.md)找到通用编辑器版本的完整列表。

## 生成变体 {#generate-variations}

您可以在[此处](/help/generative-ai/release-notes-generate-variations.md)找到生成变体版本的完整列表。

## Experience Cloud 发行说明 {#experience-cloud}

您可以在[此处](https://experienceleague.adobe.com/zh-hans/docs/release-notes/experience-cloud/current)找到有关其他 Experience Cloud 应用程序版本的信息。
