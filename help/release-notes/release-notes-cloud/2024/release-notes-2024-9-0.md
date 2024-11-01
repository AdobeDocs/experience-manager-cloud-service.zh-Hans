---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.9.0 版的发行说明。'
feature: Release Information
role: Admin
source-git-commit: 0c4db1b70aa665e1802a316ece26db1e06f40b24
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.9.0 版的发行说明 {#release-notes}

以下部分概述了 2024.9.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2022 版或 2023 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>要收到有关 Experience Cloud 发行说明更新的每月电子邮件通知，请订阅 [Adobe 优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] 作为 [!DNL Cloud Service] 的当前功能版本 (2024.9.0) 的发布日期为 2024 年 9 月 26 日。下一个功能版本 (2024.10.0) 计划于 2024 年 10 月 31 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2024 年 9 月版概述视频可了解在 2024.9.0 版中添加的功能的概要：

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新增功能 {#new-feature-sites}

#### 翻译管理 {#translation-management}

AEM 翻译工作流程和 API 操作现在可以触发事件，以提供有关翻译作业状态变化的洞察。用户可以通过 Adobe Developer Console 订阅这些事件。有关 AEM 翻译管理 API 的更多信息，请参见 [此处](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) 。

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 中的早期访问功能 {#dm-early-access}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。AI 会分析视频的音轨以转录语音并创建字幕，这些字幕可以进行编辑，以提高准确性或实现定制化。这些字幕有助于满足可访问性要求，并提高依赖或偏好基于文本的视频支持服务的观众的视频参与度。

为了尽早获得 Dynamic Media 帐户上 AI 生成的字幕支持，[请创建并提交 Adobe 客户支持案例](/help/assets/dynamic-media/video.md##enable-dash)。

### 资产选择器中的新功能 {#asset-selector-new-features}

资产选择器现在支持浏览收藏集以查找所需的资产。
![资产选择器收藏集](/help/assets/assets/collections-rail-modal-view.png)

### Content Hub 的新增强功能 {#content-hub-new-features}

管理员现在可以控制是否需要在 Content Hub 显示过期资产。如果过期的资产可见，他们还可以定义用户是否可以下载它们。

![Content Hub 上的资产已过期](/help/assets/assets/view-download-expired-assets.png)

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

* **生成自适应表单**：使用生成式 AI 提示轻松创建完整的表单。Adobe 的生成式 AI 会自动生成易于用户使用的表格，从而减少流失率，并提供个性化的体验。

* **生成表单面板**：根据特定数据收集需求生成表单中的各部分。例如，生成用于收集付款信息、客户偏好或旅行详情的部分。

* **更改表单布局**：使用生成式 AI 提示尝试使用不同的布局和设计。尝试不同的布局（如向导或选项卡视图），找到最适合您的表单的布局。使用生成式 AI 提示来优化您的表单，以实现移动响应能力，并创建用户喜爱的具有视觉吸引力的表单。

* **配置提交操作**：使用生成式 AI 提示轻松为您的表单配置提交操作。从预先构建的提交操作库或由您自己的开发团队创建和部署的自定义提交操作中进行选择。

>[!IMPORTANT]
>
> 有兴趣加入早期访问计划以体验任何有关表单方面的创新技术吗？请从您的工作邮件发送一封电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中注明您感兴趣的功能列表。

## CIF 加载项 {#cloud-services-cif}

### 改进功能 {#improvements-fixes-cif}

* 使类别限制可自定义。

### 错误修复 {#bug-fixes-cif}

* 商业字段未与资产元数据模式编辑器正确集成。
* 拖放式旋转产品多字段问题。
* 拖放式旋转产品多字段问题。
* 单击不适用于类别和产品编辑器页面上的页面信息中的菜单。
* 订单编号在订单确认页面中不可见。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 用于加载动态内容的边缘包含 (ESI) {#esi}

Adobe Managed CDN 现在支持 [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md)，这是一种用于边缘级动态 Web 内容组装的标记语言。通过加入 ESI 片段，您可以在具有更高 TTL 的 CDN 上缓存整个 HTML 页面，同时更频繁地从原始位置获取那些需要更高节奏更新（更低的 TTL）的较小部分。该功能正在逐步推出。

### CDN 上的基本身份验证 {#basicauth-cdn}

通过弹出需要用户名和密码的基本身份验证对话框来保护某些内容资源。此功能主要针对轻度身份验证用例，例如业务利益相关者审查内容，而不是作为最终用户访问权限的综合解决方案。用户名和密码列表通过Git中的配置文件进行管理，该配置文件通过配置管道部署，并引用机密类型的Cloud Manager环境变量。 [了解详情](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

### 客户端重定向 {#client-side-redirects}

在部署到CDN并在CDN上计算的配置文件Git中声明[浏览器重定向](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。 这对于删除页面、更改的网站结构和SEO优化等方案非常有用。

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎提供反馈，您可以发送电子邮件至 **<aemcs-new-devconsole-ui-beta@adobe.com>**。

![AEM Developer Console 中的 OSGi 捆绑包屏幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### 企业用户可以在 Git 之外声明重定向（早期采用者计划） {#apache-rewritemaps-early-adopter}

与 AEM 6.5 类似，Apache/dispatcher 会提取放置在发布存储库中特定位置的重写映射并对其进行加载，而无需执行 Web 层管道。这种方法让业务用户使用电子表格或 UI（如 ACS Commons Redirect Map Manager 或自定义应用程序）声明重定向。通过发送电子邮件至 **<aemcs-cdn-config-adopter@adobe.com>**&#x200B;加入早期采用者计划。

### RDE 的配置管道（早期采用者计划） {#config-pipeline-rdes-early-adopter}

[配置管道](/help/operations/config-pipeline.md)用于部署yaml文件配置，包括CDN选项（流量过滤规则、请求/响应转换等）。 通过电子邮件 **<aemcs-cdn-config-adopter@adobe.com>** 加入早期采用者计划，以将这些相同的配置部署到使用 CLI 的 RDE（快速开发环境）。

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
