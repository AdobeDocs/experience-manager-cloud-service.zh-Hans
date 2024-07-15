---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2020.10.0as a Cloud Service发行说明。"
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 24%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.10.0版发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service2020.10.0版的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.10.0的发布日期是2020年10月28日。
下一个版本(2020.11.0)将于2020年12月1日发布。

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[核心组件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)**： Adobe Experience Manager as a Cloud Service受益于对最新版本核心组件的自动更新。 版本2.12.0包括社区贡献的最新改进。 改进包括[新的POST表单处理程序；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)通过上下文感知配置包含自定义CSS、JavaScript和元数据[标记的功能；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)以及可简化自定义组件中Adobe数据层集成的[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)实用程序。 查看2.12.0中的[更改列表](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)。

* **[项目原型24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**：启动新Experience Manager项目的推荐基础有所改善。 它现在包括新的[Adobe客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、[在AMP中交付站点的选项](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html)以及添加项目CSS/JS的新[扩展点。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub文件夹](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**：能够创建受众文件夹，以便轻松组织、查找和选择要用于ContextHub产品定位功能的受众区段。

## [!DNL Adobe Experience Manager Assets]个as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]支持的视频智能标记**：通过应用AI模型来分析视频内容中的对象和特定于操作的标记，DAM用户可以减少添加标记所花费的时间，而更多时间会使用公开的、丰富的信息。 反过来，您也能为客户提供合适的体验。 请参阅[智能标记视频资产](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增强功能**： [!DNL Brand Portal]中提供了以下新增功能及更多功能。 有关详细信息，请参阅[[!DNL Brand Portal] 发行说明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [更好的下载体验](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)，使下载更简单、更快。 管理员可以配置更多下载配置，以根据用户和企业的需求提供下载体验。
   * 现在可以从任何页面一键导航到文件、[收藏集](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)和共享链接。
   * 用户现在可以[选择并下载特定呈现版本](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)。 可在“资源详细信息”页面中的“演绎版”面板中找到下载演绎版的新选项。
   * 来宾用户会话超时时间为15分钟，这可确保所有并发用户获得更好的体验。

* **[!DNL Adobe Asset Link]版本2.1**： [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]的[AdobeAsset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)扩展的新版本可用。 它增加了与2020年10月发布的版本2021的最新[!DNL Adobe Creative Cloud]应用程序的兼容性。

* **[!DNL Assets]WebP文件支持**： [!DNL Assets]as a Cloud Service现在支持WebP图像格式。 WebP是由Google创建的新兴图像格式。 WebP文件格式的图像在视觉上与JPG或PNG文件没有区别，并且文件更小。 降低资源的文件大小可缩短页面加载时间，并帮助内容创建者提供更快的Web体验。 了解如何在[创建处理配置文件](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)中使用WebP。

## [!DNL Adobe Experience Manager Forms]个as a Cloud Service {#forms-oct-2021}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）的行为，从而收集用户洞察。 它有助于商业用户根据收集的见解就自适应表单内容、布局和样式做出明智的决策。

### [!DNL Forms]预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

* **外部化AEM Workflow数据以进行安全处理**：您可以将包含敏感个人数据(SPD)元素的进程内AEM Workflow变量数据存储到客户管理的存储库中以进行安全处理。 在处理工作流时，存储在工作流变量中的数据未保留在AEM存储库中。 根据需要从客户管理的存储库中获取。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**： [通信API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html)可帮助您组合模板和XML数据以生成各种格式的文档。 该服务允许您以同步和批处理模式生成文档。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 发布了CIF Venia参考网站 — 2020.10.2，其中包括最新的CIF核心组件版本v1.4.0。有关详细信息，请参阅[CIF Venia引用站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)。

* 已发布CIF核心组件v1.4.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)。

### 错误修复 {#bug-fixes-commerce}

* 产品控制台和选取器中的GraphQL请求是通过HTTPPOST完成的。 此问题已修复，以确保Apollo GraphQL客户端遵守GraphQL客户端OSGi配置中的设置，在配置时支持GET请求。

* 对于/lib和/apps/中的配置，CIF Cloud配置UI显示“保存并关闭”按钮。 但由于这些界面是只读的，因此UI已修复为仅显示“关闭”按钮。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

Experience Manageras a Cloud Service2020.10.0中的Cloud Manager的发布日期是2020年10月2日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager“构建容器”现在支持使用Java™ 8或Java™ 11编译项目。 Maven工具链系统提供了对Java™ 11的支持。

* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的“环境”信息卡现在最多可列出三个环境。 用户可以选择&#x200B;**全部显示**&#x200B;按钮导航到“环境”摘要页面，查看包含完整环境列表的表。 有关更多信息，请参阅[查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到 Developer Console 的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到 Developer Console 不显示用于将沙盒程序的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的“取消”和“保存”选项并非一直可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 在创建项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* 环境页面有时会显示不存在的Publish和Dispatcher区段。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅[搜索工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 内容传输工具 {#content-transfer-tool}

详细了解[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 已将“时间戳”添加到提取和摄取日志。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具将跳过内容文件。
