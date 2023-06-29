---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 32fb0942b8007aeee8afa6378a9293eecd7d7700
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 42%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.6.0) 的发布日期为 2023 年 6 月 29 日。下一个功能版本(2023.7.0)计划于2023年7月27日发布。

## 发布视频 {#release-video}

请查看 2023 年 6 月发布概述视频，了解 2023.6.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 内容片段及其引用现在可以使用[内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hans)发布到 [AEM 预览服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hans#access-preview-service)，允许用户在上线前在解耦的预览应用程序上预览最终体验。
* 现在可以使用AEM GraphQL在Headless场景中为Web投放动态优化图像。 [查询变量](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) 可以在GraphQL查询中定义，以允许分离的客户端应用程序从AEM请求相应地优化的图像。
* 上的标记 [内容片段变量](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) 现在可以使用AEM GraphQL内容投放API输出到JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

**新资源视图的可用性**

此 [新建资源视图](/help/assets/assets-view-introduction.md) 现已在Experience Manager Assets中提供。 Assets View提供了简化的用户界面，使您能够轻松管理、发现和分发数字资产。 该体验面向创意人员、只读资产使用者和较轻的DAM用户。

![标记管理](/help/assets/assets/my-workspace.png)

**搜索体验增强功能**

Experience Manager Assets现在允许您从搜索结果用户界面执行更多操作：您现在可以：

* 默认情况下，在当前存储库位置内执行搜索，而不是在整个存储库中搜索关键字。

* 导航到搜索结果中显示的资产的文件夹位置。

**3D资产的缩略图预览**

[!DNL Experience Manager Assets] 现在生成 [常见3D文件格式的缩略图预览](/help/assets/file-format-support.md) 包括gLB、USDz、FBX、3DS、OBJ和SBSAR。 上传这些文件时，默认情况下会自动生成缩略图。

**链接共享配置**

改进的新用户体验，用于 [创建链接共享](/help/assets/share-assets.md) 以及一组全新的配置，管理员可通过这些配置自定义用户使用此功能的默认行为。

![标记管理](/help/assets/assets/config-email-service.png)

**Dynamic Media：更新了图像配置文件中与智能裁剪相关的字段**

图像配置文件中一些与智能裁剪相关的字段的用户界面现已更新，以反映当前定义智能裁剪的准则。 请参阅[裁切选项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=zh-Hans#crop-options)。

### Assets视图中的新增功能 {#assets-view-features}

**资产的分层标记可加快搜索体验**

随着时间的推移，受控词汇的平面列表变得难以管理。 资源视图现在支持 [分层标记结构](/help/assets/tagging-management-assets-view.md)，这有助于应用相关元数据、对资产进行分类、支持搜索、重用标记、提高可发现性等。

![标记管理](/help/assets/assets/tags-hierarchy.png)

**固定文件、文件夹和收藏集以进行快速访问**

您现在可以 [固定文件、文件夹和收藏集以加快访问速度](/help/assets/my-workspace-assets-view.md) 到这些项目（稍后需要）。 固定项目显示在 **快速访问** 部分。 您可以使用“我的工作区”访问它们，而不是导航到将它们保存在存储库中的位置。

![工作区中的“任务”](/help/assets/assets/quick-access.png)

**在垃圾桶文件夹中筛选资源**

现在通过“资源”视图，您可以 [筛选可在垃圾桶文件夹中找到的资源](/help/assets/navigate-assets-view.md). 您可以应用标准或自定义筛选条件，在垃圾桶文件夹内搜索相应的资源以恢复或永久删除它们。

**3D资产的缩略图预览**

Assets视图现在可生成常见3D文件格式（包括gLB、USDz、FBX、3DS、OBJ和SBSAR）的缩略图预览。 这些文件上传到“资产”视图后，系统会默认自动生成缩略图。

![工作区中的“任务”](/help/assets/assets/3d-preview.png)

**查看热门搜索词**

资源视图现在支持 [查看部署中的热门搜索词](/help/assets/my-workspace-assets-view.md) 使用 **分析** 部分。 您还可以导航到详细分析，以查看过去30天或12个月内的热门搜索。

![工作区中的“任务”](/help/assets/assets/insights-top-searches.png)

**元数据表单增强功能**

现在通过“资源”视图，您可以 [添加多值文本和下拉列表属性组件](/help/assets/metadata-assets-view.md#property-components) 到元数据表单。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* [AEM 页面编辑器中的自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您现在可以使用 AEM 页面编辑器快速创建多个表单并将其添加到您的 Sites 页面。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：

   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件来创建自适应表单。
   * 使用 AEM Sites 编辑器中的自适应表单向导创建独立于任何 Sites 页面的表单，让您可以自由地在多个页面中重复使用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions政府版](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms现在与面向政府的Adobe Acrobat Sign Solutions集成。 这种集成为政府型账户（政府部门和机构）的自适应表单提交提供了高级的电子签名合规性和安全性。

  与面向政府的Adobe Acrobat Sign Solutions集成使Adobe的合作伙伴和政府客户能够在Adaptive Forms中使用电子签名处理一些任务最关键和最敏感的业务线。 这层额外的安全保障机制确保所有电子签名完全符合 FedRAMP Moderate 合规性，使 Adobe 的政府客户能够安心使用。

* [在规则编辑器中使用自定义错误处理程序增强了错误处理能力](/help/forms/add-custom-error-handler-adaptive-forms.md)：您现在可以调用自定义函数（使用客户端库）来响应外部服务返回的错误，并为最终用户提供量身定制的响应。 或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后端为特定的错误代码调用自定义工作流，或者通知客户服务已停止。

  该功能有助于通过引入基于标准的错误响应来提高整体错误处理能力，这些错误响应与 OOTB 错误处理程序向后兼容，并具有更大的灵活性和控制能力。

* [表单数据模型的增强身份验证方法](/help/forms/configure-data-sources.md)：通过引入基于客户端凭据的身份验证，将AEM Forms与兼容的数据源连接，体验增强的安全性。 此增强功能消除了对模拟或用户登录的需要，增强了数据的保护。

* 使自适应Forms部分可重复：您现在可以 [可折叠项](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)， [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、和 [水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) 自适应表单的可重复组件。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  这些可重复部分允许您提供不限数量的条目，而无需固定字段计数。 当所需的数据实例事先未知时，此变量将非常有用。 Forms用户可以轻松地添加或删除部分，使表单能够适应不同的数据输入方案，并简化相同数据的多次发生收集。

### Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 [Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 使您的开发人员能够创建、发布和管理交互式表单，这些表单可通过API（而不是通过传统的图形用户界面）访问和交互。 Headless 自适应表单可帮助您：

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
