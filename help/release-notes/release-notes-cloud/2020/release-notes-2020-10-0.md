---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 作为2020.10.0的Cloud Service发行说明。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 25%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager] as a 2020.10.0的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as aCloud Service2020.10.0的发布日期是2020年10月28日。
以下版本(2020.11.0)将于2020年12月1日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* **[核心组件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)**:AEM as a Cloud Service可从自动更新最新版本的核心组件中受益。版本2.12.0包括社区提供的最新改进，如[新的POST表单处理程序；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)通过上下文感知配置包含自定义CSS、Javascript和元数据[标记的功能；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)和[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)实用程序，以简化自定义组件中的Adobe数据层集成。 请参阅2.12.0中的[更改列表](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)。

* **[项目原型24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:开始新AEM项目的推荐基础已得到改进，现在包括新的 [Adobe客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、用 [于在AMP中交付站点的选项，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 以及用于添加项 [目CSS/JS的新扩展点。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub文件夹](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:能够创建受众文件夹，以便轻松组织、查找和选择要用于ContextHub选件定位功能的受众区段。

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

* **[!DNL Adobe Sensei]启用了视频智能标记**:通过利用AI模型分析特定对象和操作标记的视频内容，DAM用户可以花费更少的时间添加标记，并更多时间利用公开的丰富信息为客户提供正确的体验。请参阅[智能标记视频资产](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增强功能**:中提供了以下新增功能及更多 [!DNL Brand Portal]功能。有关详细信息，请参阅[[!DNL Brand Portal] 发行说明](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [增强的下载](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 体验，以便简化、快速下载。管理员可以配置更多下载配置，以根据用户和企业的需求提供下载体验。
   * 现在，从任何页面都可以一键导航到“文件”、“[收藏集](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)”和“共享链接”。
   * 用户现在可以[选择并下载特定演绎版](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)。 可在“资源详细信息”页面中的“演绎版”面板中找到下载演绎版的新选项。
   * 来宾用户会话超时为15分钟，可确保所有并发用户获得更好的体验。

* **[!DNL Adobe Asset Link]版本2.1**:提供了适用于 [、和](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 的 [!DNL Adobe Photoshop]Adobe资 [!DNL Adobe Illustrator]产链接 [!DNL Adobe InDesign] 扩展的新版本。它增加了与2020年10月发布的最新[!DNL Adobe Creative Cloud]应用程序版本2021的兼容性。

* **[!DNL Assets]WebP文件支持**: [!DNL Assets] 作为Cloud Service，现在支持WebP图像格式。WebP是Google创建的一种新兴图像格式。 WebP文件格式的图像与JPG或PNG文件在视觉上没有区别，而且文件要小得多。 降低资产的文件大小缩短了页面加载时间，并帮助内容创建者提供更快的Web体验。 请参阅如何在[创建处理配置文件](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)中使用WebP 。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.10.2，其中包含最新的CIF核心组件版本v1.4.0。有关更多详细信息，请参阅[CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)。

* 已发布CIF核心组件v1.4.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)。

### 错误修复 {#bug-fixes-commerce}

* 在产品控制台中，GraphQL请求和选取器是通过HTTPPOST完成的。 已修复此问题，以确保Apollo GraphQL客户端遵循GraphQL客户端OSGi配置中的设置，以支持已配置的GET请求。

* CIF云配置UI中为/lib和/apps/中的配置显示了“保存并关闭”按钮。 但这些是只读的，因此UI已修复为仅显示“关闭”按钮。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Manager的Cloud Service2020.10.0的发布日期是2020年10月2日。

### [!DNL Cloud Manager] {#what-is-new-cm}的新增功能

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager内部版本容器现在支持使用Java 8或Java 11编译项目。 Maven工具链系统提供对Java 11的支持。

* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的“环境”卡现在最多将列出三个环境。 用户可以选择&#x200B;**显示所有**按钮以导航到“环境”摘要页以查看包含环境完整列表的表。
有关更多详细信息，请参阅[查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的取消和保存按钮并不总是可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅[搜索工作流实例](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 内容传输工具 {#content-transfer-tool}

请阅读本节内容，了解[内容传输工具](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 提取和摄取日志中添加了时间戳。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具会跳过内容文件。 此问题已修复。
