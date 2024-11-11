---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9bb2d38feea2690bc112611d429dad22e7bcd278
workflow-type: ht
source-wordcount: '1514'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的当前发行说明 {#release-notes}

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

[!DNL Adobe Experience Manager][!DNL Cloud Service]当前功能版本（2024.10.0）的释放日期是 2024 年 10 月 31 号。下一个功能版本 (2024.11.0) 计划于 2023 年 11 月 21 号释放。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**现代化页面事件**

以下 AEM Sites 页面事件现在可用作基于 AEM as a Cloud Service 事件平台的外部可用事件。可以通过 Adobe I/O 处理事件以与外部进程交互。
* 已发布页面
* 已取消发布页面
* 已删除页面

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过 AEM 的新功能[生成变体](/help/generative-ai/generate-variations.md)利用 GenAI，现在可在云服务中使用。生成变体功能可以帮助您通过使用生成式 AI 来生成和扩展内容创作。请与您的 Adobe 帐户团队联系，申请加入该项目。

**用于内容片段投放的 AEM REST OpenAPI**

用于内容片段投放的 [ AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) 现已提供给 AEM AEM as a Cloud Service 使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 中的早期访问功能 {#dm-early-access}

**AI 生成的视频字幕**

Adobe Dynamic Media 中 AI 生成的视频字幕使用人工智能为视频内容自动生成字幕。此功能旨在通过提供准确的实时字幕来提高视频的可观看性，并增强用户体验。AI 会分析视频的音轨以转录语音并创建字幕，这些字幕可以进行编辑，以提高准确性或实现定制化。这些字幕有助于满足可访问性要求，并提高依赖或偏好基于文本的视频支持服务的观众的视频参与度。

为了尽早获得 Dynamic Media 帐户上 AI 生成的字幕支持，[请创建并提交 Adobe 客户支持案例](/help/assets/dynamic-media/video.md##enable-dash)。

### 资源视图中的新增功能 {#assets-view-new-features}

**计划报告**

现在可以按照定期计划或未来日期在资产视图中自动生成报告，从而减少发现数据驱动洞察的工作量。

![Scheduled Reports-](/help/assets/assets/scheduled-reports-tab.png)

### Content Hub 的新增强功能 {#content-hub-new-features}

**已授予许可资源的 Digital Rights Management**

组织现在可以为 Content Hub 的用户利用 DRM 来获取已授予许可资源，从而提高许可证合规性并最大限度地降低共享授予许可条款资产的风险，要求用户在开始下载已授予许可资源之前先查看并接受许可条款。如需了解更多信息，请参阅 [管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

![download-multiple-license](/help/assets/assets/download-multiple-license.png)

**资源信息卡元数据配置**

Content Hub 现在允许您配置需要在资源卡信息上显示的关键元数据字段，最多 6 个字段。如需更多信息，请参阅 [配置 Content Hub ](/help/assets/configure-content-hub-ui-options.md#asset-card)中的资源信息卡分区。

![资源信息卡上的关键元数据](/help/assets/assets/asset-card-key-metadata.png)

**配置过期资源的可见性和下载**

管理员现在可以控制是否需要在 Content Hub 显示过期资源。如果过期的资源可见，他们还可以定义用户是否可以下载它们。如需更多信息，请参阅 [配置 Content Hub ](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub)中的过期资源分区。

![Content Hub 上的资产已过期](/help/assets/assets/expired-assets-content-hub.png)

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

### 错误修复 {#bug-fixes-cif}

* 修复了 UI 测试以便与 Core CIF 组件正常配合使用。
* 解决了类别 URL 格式在云实例中无法按预期运行的问题。

## [!DNL Experience Manager] 作为 [!DNL Cloud Service] 的基础 {#foundation}

### 控制表单提交的配置 {#configuration-submissions}

为了控制特定位置的 Coral 或 Foundation 表单的表单提交，AEM 引入了新的配置：`com.adobe.granite.ui.components.FormRestrict`。此配置包含两个字段：

1. **添加允许的路径**：指定允许表单操作的路径。
1. **限制行为**：确定受限路径（未包含在允许列表中的路径）的行为。您可以选择以下两个选项：
   * **弹出窗口**（默认）：显示弹出窗口通知。
   * **阻止**：阻止表单提交。

>[!NOTE]
>
>此配置不支持位于 `/apps`、 `/libs`、 `/mnt/overlay` 和  `/mnt/override` 下的所有 Coral 或 Foundation 表单。

### 具有高级网络选项的自助日志转发 {#log-forwarding}

虽然可以从 Cloud Manager 下载 AEM（包括 Apache/Dispatcher）和内容传递网络日志，但许多组织发现将这些日志流式传输到首选日志记录目的地是有益的。AEM 现在支持 [日志转发](/help/implementing/developing/introduction/log-forwarding.md) 到 Azure Blob Storage、Datadog、HTTPS、Elasticsearch（和 OpenSearch）和 Splunk。AEM 日志可以选择通过高级网络配置转发，例如使用专用的 IP 地址。

此功能由用户以自助方式配置，并使用 [配置管道](/help/operations/config-pipeline.md)进行部署。

### 面向企业用户的无管道 URL 重定向 {#pipeline-free-redirects}

当页面被删除或移动，或出现其他情况时，浏览器端重定向很有用。借助 [无管道 URL 重定向](/help/implementing/dispatcher/pipeline-free-url-redirects.md)，您可以将 Apache 重写映射文件放置在 AEM 发布位置，该文件会在该位置自动加载 - 无需将文件承诺到源代码控制或启动 Cloud Manager 管道。

发布重写文件的选项包括将其作为资源上传、使用 ACS Commons Rewrite Map Manager 或与自定义用户界面交互。

### RDE 的配置管道 {#config-pipeline-rdes}

快速开发环境是在云环境中快速部署和测试代码和配置的强大工具。RDE 现在支持 [同步配置 YAML 文件](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)，包括内容传递网络设置（例如流量筛选条件规则和请求/响应转换），以及日志转发和其他配置选项。[有关更多详细信息，请参阅受支持的配置选项的完整列表](/help/operations/config-pipeline.md)。

### 新产品轮廓 {#new-product-profiles}

创建新的 AEM 环境时，产品轮廓文件会自动出现在 Adobe Admin Console 中，从而使管理员能够分配对已授予许可解决方案和功能的访问权限。

新的环境现在包括一组更新的产品轮廓，使其与未来的功能兼容，包括在 Adobe Developer Console 中生成 API 凭据。现有环境将能够在未来的版本中更新其产品轮廓。[了解详情](/help/onboarding/aem-cs-team-product-profiles.md)。

### 新的 AEM Developer Console（公开 Beta） {#aem-developer-console-beta}

尝试改进的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，它为在云环境中调试代码提供了更具交互性的体验。

任何人都可以通过单击当前 AEM Developer Console 中的 *新控制台可用* 按钮来访问公开 Beta。Adobe 欢迎提供反馈，您可以发送电子邮件至 **<aemcs-new-devconsole-ui-beta@adobe.com>**。

![AEM Developer Console 中的 OSGi 捆绑包屏幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] Guides {#guides}

您可以找到最新版本的 Adobe Experience Manager 指南的新增功能和增强功能的完整列表 [这里](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)。

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
