---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service的2020.10.0发行说明。”'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明  {#release-notes}

以下部分概述了 [!DNL Experience Manager] as a Cloud Service2020.10.0。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0是2020年10月28日。
以下版本(2020.11.0)将于2020年12月1日发布。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[核心组件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)**:Adobe Experience Manager as a Cloud Service从最新版本的核心组件自动更新中受益。 第2.12.0版包括社区贡献的最新改进。 改进包括 [新的POST表单处理程序；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) 包含自定义CSS、JavaScript和元数据的功能 [标记；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) 和 [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) 用于简化自定义组件中Adobe数据层集成的实用程序。 请参阅 [更改列表](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) 在2.12.0中。

* **[原型24项目](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:建议的启动新Experience Manager项目的基础已得到改进。 现在，它包含了 [Adobe客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)，选项转到 [在AMP中交付站点，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 新 [扩展指向添加项目CSS/JS。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub文件夹](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:能够创建受众文件夹，以便轻松组织、查找和选择要用于ContextHub选件定位功能的受众区段。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]powered video smart标记**:通过应用AI模型来分析特定对象和操作标记的视频内容，DAM用户可以花费更少的时间添加标记，并使用公开的丰富信息花费更多的时间。 反过来，您可以为客户提供正确的体验。 请参阅 [智能标记视频资产](/help/assets/smart-tags-video-assets.md).

* **Brand Portal增强功能**:以下新增功能和更多功能在 [!DNL Brand Portal]. 有关详细信息，请参阅 [[!DNL Brand Portal] 发行说明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [增强的下载体验](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 以简化、快速的下载。 管理员可以配置更多下载配置，以根据用户和企业的需求提供下载体验。
   * 一键导航到“文件”， [收藏集](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)、和共享链接现在可从任何页面访问。
   * 用户可以 [选择和下载特定演绎版](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 现在。 可在“资源详细信息”页面中的“演绎版”面板中找到下载演绎版的新选项。
   * 来宾用户会话超时为15分钟，可确保所有并发用户获得更好的体验。

* **[!DNL Adobe Asset Link]版本2.1**:的新版本 [Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html) 扩展 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign] 中。 它增加了与最新版本的兼容性 [!DNL Adobe Creative Cloud] 2020年10月发布的2021版应用程序。

* **[!DNL Assets]WebP文件支持**: [!DNL Assets] as a Cloud Service现在支持WebP图像格式。 WebP是由Google创建的一种新兴图像格式。 WebP文件格式的图像与JPG或PNG文件在视觉上没有区别，而且文件要小得多。 降低资产的文件大小缩短了页面加载时间，并帮助内容创建者提供更快的Web体验。 了解如何在 [创建处理配置文件](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **适用于自适应Forms的Analytics**:现在，您可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）的行为，以收集最终用户分析。 它有助于企业用户根据收集到的洞察信息，就自适应表单内容、布局和样式做出明智的决策。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

* **将AEM工作流数据外部化以进行安全处理**:您可以将包含敏感个人数据(SPD)元素的正在处理的AEM工作流变量数据存储在客户管理的存储库中，以便进行安全处理。 处理工作流时，存储在工作流变量中的数据不会保留在AEM存储库中。 它是按需从客户管理的存储库获取的。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=zh-Hans) 帮助您将模板和XML数据结合起来，以生成各种格式的文档。 该服务允许您以同步和批处理模式生成文档。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.10.2，其中包含最新的CIF核心组件版本v1.4.0。请参阅 [CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 以了解更多详细信息。

* 已发布CIF核心组件v1.4.0。请参阅 [CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) 以了解更多详细信息。

### 错误修复 {#bug-fixes-commerce}

* 产品控制台和选取器中的GraphQL请求是通过HTTPPOST完成的。 此问题已修复，以确保Apollo GraphQL客户端遵循GraphQL客户端OSGi配置中的设置，以支持已配置的GET请求。

* CIF云配置UI中为/lib和/apps/中的配置显示了“保存并关闭”按钮。 但这些界面是只读的，因此UI已修复为仅显示“关闭”按钮。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

Cloud Manager在Experience Manageras a Cloud Service中的发布日期为2020.10.0 2020年10月2日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager的“生成容器”现在支持使用Java™ 8或Java™ 11编译项目。 Maven工具链系统提供对Java™ 11的支持。

* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的“环境”卡现在最多可列出三个环境。 用户可以选择 **显示全部** 按钮以导航到“环境摘要”页以查看包含环境完整列表的表。
请参阅 [查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 以了解更多详细信息。

### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的取消和保存按钮并不总是可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页面有时会显示不存在的发布区段和Dispatcher区段。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅 [搜索工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## 内容传输工具 {#content-transfer-tool}

进一步了解的新增功能和更新 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 提取和摄取日志中添加了时间戳。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具会跳过内容文件。
