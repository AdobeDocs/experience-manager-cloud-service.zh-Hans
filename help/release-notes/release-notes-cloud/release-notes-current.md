---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 5995c416328e6f340285004ec2e723cc9279dabd
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 49%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2023.7.0)为2023年7月27日。 下一个功能版本(2023.8.0)计划于2023年8月31日发布。

## 发布视频 {#release-video}

请查看 2023 年 7 月发布概述视频，了解 2023.7.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 内容片段的MSM。 AEM多站点管理器现在可用于内容片段，允许创建内容片段活动副本以进行批量内容分发。 粒度继承控件可精确到内容片段元素和变体级别使用。

### [!DNL Experience Manager Sites] 预发行版本中的新增功能 {#prerelease-sites}

* 此 [内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hans) 现在允许用户查看标记，并按作为元数据应用于内容片段的标记进行搜索。 用户不再需要切换到Assets UI即可实现此功能，从而减少上下文切换并提高效率。

![在内容片段控制台中标记](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**适用于图像智能标记的改进的人工智能框架**

Experience Manager Assets 现在为图像智能标记使用改进的人工智能框架。这种内容智能化可提高智能标记的相关性和准确性，可用于摄取的所有图像资源。

**配置资源列表视图的列显示**

Assets Essentials 现在可让您选择资源列表视图中显示的列，例如“状态”、“格式”、“维度”、“大小”等。

![配置列](/help/release-notes/assets/configure-columns.png)

**根据相关性对搜索结果进行排序**

默认情况下，Assets Essentials 现在根据相关性对搜索结果进行排序。可按 `Name`、`Relevance`、`Size`、`Modified` 和 `Created` 的升序或降序为搜索到的资源排序。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-forms-channel}

* [**现成主题**](/help/forms/using-themes-in-core-components.md) **和模板**：利用我们现成的OOTB主题和模板启动表单创建流程，这些主题和模板经过定制，可增强经验丰富的专业人员和新表单作者的能力。 通过无缝使用自适应Forms核心组件构建，这些精心策划的主题和模板允许您为常见用例快速创建表单。

  ![现成模板](/help/forms/assets/form-templates-ootb.png)

* **适用于Headless Forms的React组件**：您现在可以使用现成的React组件预览和自定义Headless自适应表单演绎版。 这些组件利用自适应Forms核心组件的BEM类进行样式设置，使您能够轻松根据特定要求自定义其外观。

* [**创建包含可重复部分的自适应Forms**](/help/forms/create-forms-repeatable-sections.md)：您现在可以制作 [折叠](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)， [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、和 [水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) 可重复用于多个数据记录捕获的基于组件的自适应表单。  这些可重复部分允许您轻松提供多个数据条目。 当预先未知所需的数据实例时，它非常有用。表单填充器可以轻松地添加或移除部分，使表单适应不同的数据输入方案，并简化相同数据记录的多个发生次数的收集。


### 中提供的预发行版功能 [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA企业支持**](/help/forms/captcha-adaptive-forms.md)：在自适应表单中使用Google reCAPTCHA Enterprise可增强对欺诈活动和垃圾邮件的保护，从而提供更安全的用户体验。 借助高级风险分析和无缝集成，正版用户可以轻松地提交表单，同时有效地阻止机器人。

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

订阅电子邮件通知，在发生需要立即采取行动的严重事件时提醒您，并提供个性化推荐以优化您的站点。 [操作中心](/help/operations/actions-center.md) 用作中心位置，您可以在此查看这些警报（例如已阻止的复制队列或即将过期的凭据），并将它们标记为已解决。

![操作中心屏幕截图](/help/assets/assets/actions-center.png)

### CDN和WAF规则早期采用者计划 {#waf-early-adopter}

筛选CDN上的流量，依据：
* 请求标头和属性（如IP地址）
* 已知与恶意通信相关联的通信模式

有兴趣试用该功能并分享反馈吗？ 发送电子邮件至 **aemcs-waf-adopter@adobe.com** 从您的官方电子邮件ID了解有关率先采用者计划的更多信息。 空间有限。

在文章中了解有关该功能的更多信息 [此处](/help/security/cdn-and-waf-rules.md).

### 其他基础更改 {#other-foundation-changes}

* 在8月7日当周，对AEM实例的请求超过正常级别时，AEM将返回错误代码429，而不是错误代码503。 [了解详情](/help/implementing/developing/introduction/development-guidelines.md).

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
