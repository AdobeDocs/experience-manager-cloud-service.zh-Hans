---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.6.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.6.0 版的发行说明。'
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
feature: Release Information
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.6.0 版的发行说明 {#release-notes}

以下部分概述了 2023.6.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.6.0) 的发布日期为 2023 年 6 月 29 日。下一个功能版本 (2023.7.0) 计划于 2023 年 7 月 27 日发布。

## 发布视频 {#release-video}

请查看 2023 年 6 月发布概述视频，了解 2023.6.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 内容片段及其引用现在可以使用[内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)发布到 [AEM 预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)，允许用户在上线前在解耦的预览应用程序上预览最终体验。

![在内容片段控制台中预览](/help/assets/content-fragments-console-preview.png)

* 现在可以使用 AEM GraphQL 在 Headless 场景中动态优化图像以实现 Web 交付。[查询变量](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html#query-variables)可以在 GraphQL 查询中定义，以允许解耦的客户端应用程序从 AEM 请求相应优化的图像。
* [内容片段变体](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html)上的标记现在可以使用 AEM GraphQL 内容交付 API 将其输出为 JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

**新的资源视图的可用性**

[新的资源视图](/help/assets/assets-view-introduction.md)现已在 Experience Manager Assets 中提供。资源视图提供简化的用户界面，使您可以轻松管理、探索和分发数字资源。 该体验面向创意人员、只读资源消费者和轻量级 DAM 用户。

![标记管理](/help/assets/assets/my-workspace.png)

**搜索体验增强**

Experience Manager Assets 现在使您能够通过搜索结果用户界面执行更多操作：您现在可以：

* [默认情况下在当前存储库位置内执行搜索，而不是在整个存储库中搜索关键字。](/help/assets/search-assets.md)

* [导航到搜索结果中显示的资源的文件夹位置。](/help/assets/search-assets.md#aftersearch)

**3D 资源的缩略图预览**

[!DNL Experience Manager Assets] 现在可以生成常见 3D 文件格式的缩略图预览，包括 gLB、USDz、FBX、3DS、OBJ 和 SBSAR。[](/help/assets/file-format-support.md)当这些文件上传时，默认情况下会自动生成缩略图。

**Dynamic Media：更新了图像配置文件中与智能裁剪相关的字段**

图像配置文件中一些与 Smart Crop 相关的字段的用户界面现已更新，可反映当前定义 Smart Crop 的指南。请参阅[裁切选项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html#crop-options)。

### 资源视图中的新增功能 {#assets-view-features}

**资源的分层标记可提供更快的搜索体验**

随着时间的推移，受控词汇的扁平列表变得难以管理。资源视图现在支持[分层的标记结构](/help/assets/tagging-management-assets-view.md)，该结构便于应用相关的元数据、为资源分类、支持搜索、重用标记、提高可发现性等。

![标记管理](/help/assets/assets/tags-hierarchy.png)

**固定文件、文件夹和集合以便快速访问**

您现在可以[固定文件、文件夹和集合，以便在以后需要时更快地访问](/help/assets/my-workspace-assets-view.md)这些项目。经过固定的项目都显示在“我的工作区”的&#x200B;**快速访问**&#x200B;部分。您可以使用“我的工作区”访问它们，而无需导航到存储库中保存它们的位置。

![工作区中的“任务”](/help/assets/assets/quick-access.png)

**过滤“垃圾箱”文件夹中的资源**

现在通过资源视图可以[筛选“垃圾箱”文件夹中的资源。](/help/assets/navigate-assets-view.md)您还可以应用标准或自定义过滤器来搜索“垃圾箱”文件夹中的相应资源，以恢复或永久删除它们。

**3D 资源的缩略图预览**

资源视图现在可以生成常见 3D 文件格式的缩略图预览，包括 gLB、USDz、FBX、3DS、OBJ 和 SBSAR。当这些文件上传到资源视图时，默认情况下系统会自动生成缩略图。

![工作区中的“任务”](/help/assets/assets/3d-preview.png)

**查看热门搜索词**

现在支持使用“我的工作区”的&#x200B;**“见解”**&#x200B;部分[查看资源视图部署](/help/assets/my-workspace-assets-view.md)中搜索最多的术语。您还可以访问详细的见解，以查看过去 30 天或 12 个月内的热门搜索。

![工作区中的“任务”](/help/assets/assets/insights-top-searches.png)

**元数据表单增强功能**

资源视图现在允许您[向元数据表单添加多值文本和下拉列表属性组件。](/help/assets/metadata-assets-view.md#property-components)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* [AEM 页面编辑器中的自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您现在可以使用 AEM 页面编辑器快速创建多个表单并将其添加到您的 Sites 页面。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：

   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件来创建自适应表单。
   * 使用 AEM Sites 编辑器中的自适应表单向导创建独立于任何 Sites 页面的表单，让您可以自由地在多个页面中重复使用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign 解决方案政府版](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms 现在可与 Adobe Acrobat Sign 解决方案政府版集成。这种集成为政府型账户（政府部门和机构）的自适应表单提交提供了高级的电子签名合规性和安全性。

  与 Adobe Acrobat Sign 解决方案政府版的集成使 Adobe 的合作伙伴和政府客户能够在一些最关键和敏感的业务领域使用自适应表单中的电子签名功能。这层额外的安全保障机制确保所有电子签名完全符合 FedRAMP Moderate 合规性，使 Adobe 的政府客户能够安心使用。

* [增强了使用规则编辑器中的自定义错误处理程序处理错误的功能：您现在可以调用自定义函数（使用客户端库）来响应外部服务返回的错误，并为最终用户提供量身定制的响应，或对服务返回的错误采取特定操作，并为最终用户提供量身定制的响应。](/help/forms/add-custom-error-handler-adaptive-forms.md)或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后端为特定的错误代码调用自定义工作流，或者通知客户服务已停止。

  该功能有助于通过引入基于标准的错误响应来提高整体错误处理能力，这些错误响应与 OOTB 错误处理程序向后兼容，并具有更大的灵活性和控制能力。

* [增强了表单数据模型的身份验证方法](/help/forms/configure-data-sources.md)：通过引入基于客户端凭据的身份验证来将 AEM Forms 与兼容的数据源连接起来，体验更高的安全性。此增强功能消除了模拟或用户登录的需要，从而增强了对数据的保护。

* [具有可重复部分的自适应表单](/help/forms/create-forms-repeatable-sections.md)：现在可在基于核心组件的自适应表单中放置[可折叠项](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)、[面板](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)和[水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)组件，以创建可重复的部分。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  这些可重复的部分允许您提供无限数量的条目，而无需固定的字段数。当预先未知所需的数据实例时，它非常有用。Forms 用户可以轻松添加或删除相关部分，使表单可适应不同的数据输入场景，并简化对同一数据发生次数的收集。

* **[将自适应表单提交到 Microsoft® SharePoint 和 Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：提高业务用户的敏捷性，以快速启用新表单并将提交的数据存储在日常使用工具中，例如 Microsoft® SharePoint 站点或 OneDrive 文件夹。

### Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 [Headless 自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用 Adobe Experience Manager Forms 的强大功能

您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
