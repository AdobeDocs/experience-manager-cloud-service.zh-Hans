---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2020.9.0版as a Cloud Service发行说明。"
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.9.0版发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service2020.9.0版的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.9.0的发布日期是2020年9月24日。

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 单页应用程序(SPA)编辑器JavaScript SDK [现在是开放源代码](/help/implementing/developing/hybrid/reference-materials.md)。

## [!DNL Adobe Experience Manager Assets]个as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 通过资源微服务生成的演绎版支持对图像文件添加水印。 它可以配置为处理配置文件，并使用PNG文件作为水印。 请参阅[为您的资产添加水印](/help/assets/watermark-assets.md)。

* [!DNL Dynamic Media]中的增强功能

   * 选择性Publish — 营销团队现在可以访问同步到[!DNL Dynamic Media]的[!DNL Dynamic Media]智能裁剪图像和动态演绎版，以便创建促销材料，而无需将这些资源发布到[!DNL Dynamic Media]进行全球交付。 [!DNL Experience Manager]和[!DNL Dynamic Media]发布是分离的，可单独进行以实现这一点。 请参阅[选择性发布](/help/assets/dynamic-media/selective-publishing.md)。
   * 管理员现在可以重置在预配时收到的[!DNL Dynamic Media]Cloud Service密码。 重置可在[!DNL Experience Manager]用户界面中完成，无需使用[!DNL Dynamic Media Classic]桌面应用。

* 要了解以下增强功能，请参阅[Brand Portal中的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans)。

   * Adobe Document CloudPDFSDK集成的增强型视图预览。
   * 单击下载功能。
   * 下载体验的新管理配置。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF核心组件v1.3.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0)。

* 产品和类别模板的产品/类别预览功能现已可用。 这允许AEM中的业务用户/营销人员查看包含真实数据的产品/类别模板。

* 产品和类别中添加了属性页面，以允许业务用户查看与产品SKU/类别ID关联的详细信息。

* 产品控制台中添加了排序功能，以允许按名称或价格属性对产品/类别进行排序。

* 产品搜索功能已添加到产品控制台。

### 错误修复 {#bug-fixes-commerce}

* Commerce Cloud配置不遵循继承。 此问题已得到修复，以确保配置继承值。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

[!UICONTROL Cloud Manager]版本2020.9.0的发布日期是2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核已重新标记为体验审核。
* 构建过程分为三个单独的 Maven 命令。
* 如果 Git 存储库无法克隆，则最多允许重复尝试三次。

### 错误修复 {#bug-fixes-cm}

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本 URL。

## 云就绪分析器 {#cloud-readiness-analyzer}

阅读本节内容，了解Cloud Readiness Analyzer v1.1.0版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer (CRA)具有启动状态控制台，该控制台显示一个明确的&#x200B;**生成报告**&#x200B;按钮，供用户单击以执行CRA。

* CRA UI在运行时会显示进度。 它显示正在分析的项目以及在执行过程中找到的结果。

* CRA报告以表格形式显示了调查结果的摘要和数量，按调查结果类型和重要性级别进行整理。 单击该调查结果的编号将自动滚动到该调查结果在报告中的位置。

### 错误修复 {#cra-bug-fixes}

* 在某些情况下，在强制刷新后，CRA报表不会更新。 此版本中已修复此问题。

## 内容传输工具 {#content-transfer-tool}

阅读本节内容，了解内容传输工具版本v1.1.10的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)支持Azure Blob Store数据存储。

* CTT用户界面具有自动重新加载功能，每30秒重新加载一次概述页面。

* CTT用户界面中添加了按钮，以便轻松检索&#x200B;*访问令牌*。

* 为&#x200B;*URL*&#x200B;和&#x200B;*迁移集名称*&#x200B;添加了描述性验证消息。

## 代码重构工具 {#code-refactoring}

阅读本节内容，了解代码重构工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI插件支持Repository Modernizer，并允许用户使用插件执行该工具。

  有关更多详细信息，请参阅[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)。

* Repository Modernizer实用程序可用于将现有项目包重构为与为AEM as a Cloud Service定义的项目结构兼容的包。

  有关更多详细信息，请参阅[Git资源：存储库现代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
