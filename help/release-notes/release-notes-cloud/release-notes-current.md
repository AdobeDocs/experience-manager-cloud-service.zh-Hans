---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] cloud service发行说明。'
translation-type: tm+mt
source-git-commit: 65752c7c51538de27aa2b21695e8eb6c6695a5f5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## 发布日期 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
以下版本(2020.11.0)将于2020年12月1日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **原型24工程**:开始新AEM项目的推荐基础更好，现在包括新的Adobe客户端数据层、以AMP形式传送站点的选项以及添加项目CSS/JS的新扩展点。

* **ContextHub文件夹**:能够创建受众文件夹，以便轻松组织、查找和选择受众区段，以用于ContextHub优惠定位功能。

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]强大的视频智能标记**:通过利用AI模型分析针对对象和特定操作标记的视频内容，DAM用户可以花费更少的时间添加标记，并将更多时间用于利用暴露的丰富信息向客户提供正确的体验。 请参 [阅智能标记视频资源](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增强功能**:中提供了以下新增功能等 [!DNL Brand Portal]。 For details, see [[!DNL Brand Portal] release notes](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [增强的下载体验](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) ，简化、快速下载。 管理员可以配置其他下载配置，以优惠适合用户和企业需求的体验。
   * 现在，可以从任何页面一键 [导航](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)到文件、集合和共享链接。
   * 用户现 [在可以选择和下载特定](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 再现。 新的演绎版下载选项位于资产详细信息页面的演绎版面板中。
   * 来宾用户会话超时15分钟可确保为所有并发用户提供更好的体验。

* **[!DNL Adobe Asset Link]2.1版**:有新版本的 [Adobe资产](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)[!DNL Adobe Photoshop]链接扩展， [!DNL Adobe Illustrator]并提 [!DNL Adobe InDesign] 供了该扩展。 它增加了与2020年10月发 [!DNL Adobe Creative Cloud] 布的2021版最新应用程序的兼容性。

* **[!DNL Assets]WebP文件支持**: [!DNL Assets] 作为Cloud Service，现在支持WebP图像格式。 WebP是由谷歌创建的一种新兴的图像格式。 WebP文件格式的图像在视觉上与JPG或PNG文件无明显区别，并且文件要小得多。 降低资产的文件大小可缩短页面加载时间，并帮助内容创建者交付更快的Web体验。 请参 [阅创建标准处理用户档案](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考站点- 2020.10.2，其中包括最新CIF核心组件版本v1.4.0。有关更多详 [细信息，请参阅CIF Venia参考站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 。

* 已发布CIF核心组件v1.4.0。有关更多详 [细信息，请参阅](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) CIF核心组件。

### 错误修复 {#bug-fixes-commerce}

* 产品控制台中的GraphQL请求和选择器是通过HTTPPOST完成的。 此问题已得到修复，以确保Apollo GraphQL客户端遵循GraphQL客户端OSGi配置中的设置，以在配置后支持GET请求。

* CIF云配置UI为/lib和/apps/中的配置显示“保存并关闭”按钮。 但这些是只读的，因此UI被修复为仅显示“关闭”按钮。

## Cloud Manager {#cloud-manager}

* 环境页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager构建容器现在支持使用Java 8或Java 11编译项目。 Maven工具链系统提供对Java 11的支持。

* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的环境卡现在最多可列表三个环境。 用户可以选择 **显示全部** 按钮，导航到环境摘要页面以视图具有完整环境列表的表。
有关更多 [详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) ，请参阅查看环境。

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

* 增加了根据工作流标题、工作流模型、状态、发起者、有效负荷路径和开始日期搜索工作流实例的支持。 请参阅 [搜索工作流实例](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 内容传输工具 {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 添加到提取和摄取日志的时间戳。 添加的消息，指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径与文件名部分相似，则内容传输工具将跳过内容文件。 已修复。
