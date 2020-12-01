---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] cloud service发行说明。'
translation-type: tm+mt
source-git-commit: 841069f35539a49c6ee67699bf3a476cf1c9da41
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 17%

---



# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版的发行说明 {#release-notes}

以下部分概述了作为2020.10.0Cloud Service的[!DNL Experience Manager]的一般发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2020.10.0的发布日期为2020年10月28日。
以下版本(2020.11.0)将于2020年12月1日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* **[核心组件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**:AEM作为Cloud Service，可从对最新版核心组件进行自动更新中受益。版本2.12.0包括社区提供的最新改进，如[新的POST表单处理程序；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)通过上下文感知配置包含自定义CSS、Javascript和元数据[标签的能力；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)和[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)实用程序，以简化自定义组件中Adobe数据层的集成。 请参阅2.12.0中[更改列表](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)。

* **[原型24工程](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:开始新AEM项目的推荐基础更好，现在包括新的 [Adobe客户端层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、以AMP形 [式传送站点的选](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 项，以及 [添加项目CSS/JS的新扩展点。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub文件夹](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:能够创建受众文件夹，以便轻松组织、查找和选择受众区段，以用于ContextHub优惠定位功能。

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service  {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

* **[!DNL Adobe Sensei]强大的视频智能标记**:通过利用AI模型分析针对对象和特定操作标记的视频内容，DAM用户可以花费更少的时间添加标记，并将更多时间用于利用暴露的丰富信息向客户提供正确的体验。请参阅[智能标记视频资产](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增强功能**:中提供了以下新增功能等 [!DNL Brand Portal]。有关详细信息，请参阅[[!DNL Brand Portal] 发行说明](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [增强的下](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 载体验，简化、快速下载。管理员可以配置其他下载配置，以优惠适合用户和企业需求的体验。
   * 现在，只需单击一下即可从任何页面导航到文件、[集合](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)和共享链接。
   * 用户现在可以[选择并下载特定的演绎版](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)。 新的演绎版下载选项位于资产详细信息页面的演绎版面板中。
   * 来宾用户会话超时15分钟可确保为所有并发用户提供更好的体验。

* **[!DNL Adobe Asset Link]2.1版**:有适用于和 [的新](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 版Adobe资 [!DNL Adobe Photoshop]产 [!DNL Adobe Illustrator]Linkextension的 [!DNL Adobe InDesign] 资产。它增加了与2020年10月发布的最新[!DNL Adobe Creative Cloud]应用程序与版本2021的兼容性。

* **[!DNL Assets]WebP文件支持**: [!DNL Assets] 作为Cloud Service，现在支持WebP图像格式。WebP是由谷歌创建的一种新兴的图像格式。 WebP文件格式的图像在视觉上与JPG或PNG文件无明显区别，并且文件要小得多。 降低资产的文件大小可缩短页面加载时间，并帮助内容创建者交付更快的Web体验。

<!--
### Bugs Fixed {#bugs-fixed-assets}

Content to come
-->

## Adobe Experience Manager商务作为Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考站点- 2020.10.2，其中包括最新CIF核心组件版本v1.4.0。有关更多详细信息，请参阅[CIF Venia参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)。

* 已发布CIF核心组件v1.4.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)。

### 错误修复 {#bug-fixes-commerce}

* 产品控制台中的GraphQL请求和选择器是通过HTTPPOST完成的。 此问题已得到修复，以确保Apollo GraphQL客户端遵循GraphQL客户端OSGi配置中的设置，以在配置后支持GET请求。

* CIF云配置UI为/lib和/apps/中的配置显示“保存并关闭”按钮。 但这些是只读的，因此UI被修复为仅显示“关闭”按钮。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service2020.10.0的发布日期为2020年10月2日。

### [!DNL Cloud Manager] {#what-is-new-cm}中的新增功能

* 环境页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager构建容器现在支持使用Java 8或Java 11编译项目。 Maven工具链系统提供对Java 11的支持。


* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的环境卡现在最多可列表三个环境。 用户可以选择&#x200B;**显示全部**按钮，导航到环境摘要页面，以视图具有完整环境列表的表。
有关详细信息，请参阅[查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* “非生产管道编辑”页面上的“取消”和“保存”按钮并不总是可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 增加了根据工作流标题、工作流模型、状态、发起者、有效负荷路径和开始日期搜索工作流实例的支持。 请参阅[搜索工作流实例](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 内容传输工具 {#content-transfer-tool}

可查看本节以了解[内容传输工具](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 添加到提取和摄取日志的时间戳。 添加的消息，指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径与文件名部分相似，则内容传输工具将跳过内容文件。 已修复。

