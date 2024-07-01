---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.7.0 版的发行说明。'
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
feature: Release Information
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: ht
source-wordcount: '896'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.7.0 版的发行说明 {#release-notes}

以下部分概述了 2023.7.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.7.0) 的发布日期为 2023 年 7 月 27 日。下一个功能版本 (2023.8.0) 计划于 2023 年 8 月 31 日发布。

## 发布视频 {#release-video}

请观看 2023 年 7 月发布概述视频，大致了解 2023.7.0 版本中的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 内容片段的 MSM。AEM Multisite Manager 现已可用于内容片段，使您能够创建内容片段 Live Copy 以进行批量内容分发。精细的继承控制可向下细化至内容片段元素和变体级别。

### [!DNL Experience Manager Sites] 预发行版本中的新增功能 {#prerelease-sites}

* [内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html)现在允许用户查看标记并按作为元数据应用于内容片段的标记进行搜索。用户将不再需要切换到此功能的资源 UI，这减少了上下文切换并提高了效率。

![内容片段控制台中的标记](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**为图像智能标记改进了人工智能框架**

Experience Manager Assets 现在使用为图像智能标记改进的人工智能框架。这种内容情报可提高对摄取的所有图像资源都可用的智能标记的相关性和准确性。

**配置显示“资源列表”视图的各列的方式**

Assets Essentials 现在让您可选择在“资源列表”视图中显示的列，如“状态”、“格式”、“维度”、“大小”等。

![配置各列](/help/release-notes/assets/configure-columns.png)

**根据相关性为搜索结果排序**

Assets Essentials 现在默认情况下根据相关性为搜索结果排序。可按 `Name`、`Relevance`、`Size`、`Modified` 和 `Created` 的升序或降序为搜索到的资源排序。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-forms-channel}

* [**现成的主题**](/help/forms/using-themes-in-core-components.md)**和模板**：使用我们现成的 OOTB 主题和模板开始您的表单创建过程，这些主题和模板专为经验丰富的专业人士和新表单作者定制。这些精心策划的主题和模板是使用自适应表单核心组件无缝构建的，可让您快速开始为常见用例创建表单。

* **[Headless 表单的 React 组件](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**：您现在可以使用现成的 React 组件预览和自定义 Headless 自适应表单演绎版。这些组件使用自适应表单核心组件中的 BEM 类进行样式设置，使您能够轻松地根据特定要求自定义其外观。

* [**创建具有可重复部分的自适应表单**](/help/forms/create-forms-repeatable-sections.md)：现在可使基于自适应表单的[可折叠项](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)、[面板](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)和[水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)组件能够对多数据记录捕获重复。这些可重复的部分可让您轻松提供多个数据条目。当预先未知所需的数据实例时，它非常有用。表单填写者可以轻松添加或删除相关部分，使表单能够适应不同的数据输入场景，并简化对同一数据记录发生次数的收集。


### [!DNL Forms] 中的预发布功能 {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA 企业支持**](/help/forms/captcha-adaptive-forms.md)：在自适应表单中使用 Google reCAPTCHA Enterprise 以增强对欺诈活动和垃圾邮件的防御，从而提供更安全的用户体验。借助高级风险分析和无缝集成，真实用户可以轻松提交表单，同时有效阻止机器人。

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 [Headless 自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用 Adobe Experience Manager Forms 的强大功能

您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。

## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### 操作中心 {#actions-center}

订阅电子邮件通知，以便在发生需要立即采取措施的重大事件时收到提醒，并获得个性化建议以优化您的网站。在[操作中心](/help/operations/actions-center.md)中，您可以查看这些提醒，例如复制队列受阻或凭据过期，并将它们标记为已解决。

![操作中心屏幕快照](/help/assets/assets/actions-center.png)

### CDN 和 WAF 规则早期采用者计划 {#waf-early-adopter}

基于以下项筛选 CDN 上的流量：
* 请求标头和属性（例如，IP 地址）
* 已知与恶意流量相关的流量模式

想试用该功能并分享反馈吗？使用您的官方电子邮件 ID 将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，了解有关早期采用者计划的更多信息。空间是有限的。

在[此处](/help/security/traffic-filter-rules-including-waf.md)的文章中详细了解该功能。

### 其他 Foundation 更改 {#other-foundation-changes}

* 在 8 月 7 日这一周，当对 AEM 实例的请求超出正常水平时，AEM 将返回错误代码 429 而不是错误代码 503。[了解详情](/help/implementing/developing/introduction/development-guidelines.md)。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
