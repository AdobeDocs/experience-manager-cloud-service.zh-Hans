---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.8.0 版的发行说明。'
feature: Release Information
role: Admin
source-git-commit: 35ec3edfec42936b9a5908265d6dbb529a70f6cf
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.8.0 版的发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2022 版或 2023 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2024.8.0) 的发布日期为 2024 年 8 月 29 日。下一个功能版本 (2024.9.0) 计划于 2024 年 9 月 26 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看 2024 年 8 月发行版概述视频，了解 2024.8.0 版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#new-feature-sites}

**适用于 Edge Delivery Services 的 AEM 创作**

现在支持现有 Sites [继承](/help/sites-cloud/authoring/universal-editor/inheritance.md)功能，包括：

* [AEM 启动项](/help/sites-cloud/authoring/launches/overview.md)
* 页面级别的 [MSM](/help/sites-cloud/administering/msm/overview.md)

此外，现在还支持以下页面管理功能：

* [AEM 标记](/help/sites-cloud/authoring/sites-console/tags.md)可以作为一项[分类法](/help/edge/wysiwyg-authoring/taxonomy.md)导出至 Edge Delivery Services。
* Edge Delivery Services 的[模板](/help/edge/wysiwyg-authoring/templates.md)即将推出！

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets 视图中的新增功能 {#assets-view-new-features}

**更新了 Adobe Firefly 图像生成**

Assets as a Cloud Service 现在可以使用 Firefly 的最新小组件，以便您使用 Adobe Firefly 生成不同风格的图像。通过使用内置的 Firefly 编辑器定义其样式、构成、维度等，您可以直接在 AEM Assets 存储库中快速创建和保存所需的资产，以供立即使用。

![Adobe Firefly 图像生成](/help/assets/assets/bugatti-type-57.png)

**PSB 文件支持**

除了现有的 PSD 文件支持功能外，Assets as a Cloud Service 现在还支持 Photoshop 大文档（PSB 文件）。

### Content Hub 的新增强功能 {#content-hub-new-enhancements}

* 更好地处理长文件名，可以通过工具提示轻松扩展完整名称。
* 改进了缩略图，以更好地适应内容纵横比，并覆盖更大面积的内容。
* Content Hub 支持 AEM 的自定义缩略图体验。
* 改进了颜色搜索功能。
* 改进了配置保存体验。
* 改进了收藏集的信息页面，以反映创作者的姓名。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 预发行版中的新功能 {#forms-new-prerelease-features}

#### 自动保存基于核心组件的自适应表单草稿

用户现在可以享受自动保存功能，该功能可以自动将部分完成的表格保存为草稿。他们可以稍后返回同一设备或其他设备来完成填写。此功能通过减少表单放弃来提高组织的转化率，因为用户不需要从头开始填写表单。


### AEM Forms 中的早期访问功能 {#forms-new-early-access-features}

AEM Forms Early Access Program 项目为您提供了一个独特的机会，让您可以独家访问尖端创新技术，并帮助塑造其发展。

本发行说明列出了当前版本提供的创新功能。有关 Early Access Program 下可用创新功能的完整列表，请参阅 [AEM Forms Early Access Program 文档](/help/forms/early-access-ea-features.md)。

#### AEM Forms AI 助手

自适应表单的生成式 AI 为您的表单开发流程带来了全新的强大功能和便捷性。它使您能够比以往更快地构建更优质的表单。

![生成式 AI 助手、自适应表单](/help/forms/assets/generative-ai-assistant.png)

我们提供的生成式 AI 功能包括：

* **产品查询 AI 助手**：立即获得与 AEM 表单相关的问题的答案。AI 助手可以充当您自己的个人知识库，能够直接在平台内提供富有洞察力的指导和建议。

* **生成自适应表单**：使用生成式 AI 提示轻松创建完整的表单。我们的生成式 AI 会自动生成易于用户使用的表格，从而减少流失率，并提供个性化的体验。

* **生成表单面板**：根据特定数据收集需求生成表单中的各部分。例如，生成用于收集付款信息、客户偏好或旅行详情的部分。

* **更改表单布局**：使用生成式 AI 提示尝试使用不同的布局和设计。尝试不同的布局（如向导或选项卡视图），找到最适合您的表单的布局。使用生成式 AI 提示来优化您的表单，以实现移动响应能力，并创建用户喜爱的具有视觉吸引力的表单。

* **配置提交操作**：使用生成式 AI 提示轻松为您的表单配置提交操作。从预先构建的提交操作库或由您自己的开发团队创建和部署的自定义提交操作列表中进行选择。

>[!IMPORTANT]
>
> 如果您有兴趣加入任何创新技术的早期访问项目，以获取有关任何创新的信息，您只需通过您的官方电子邮件地址向 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 发送一封电子邮件，并附上您感兴趣的功能列表即可。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

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
