---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service的2020.9.0发行说明。”'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版的发行说明  {#release-notes}

以下部分概述了 [!DNL Experience Manager] as a Cloud Service2020.9.0。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.9.0是2020年9月24日。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 单页应用程序 (SPA) 编辑器 JavaScript SDK [现已开源](/help/implementing/developing/hybrid/reference-materials.md)。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 通过资产微服务生成的演绎版支持对图像文件添加水印。 它可以配置为处理配置文件，并使用PNG文件作为水印。 请参阅 [对资产添加水印](/help/assets/watermark-assets.md).

* 中的增强功能 [!DNL Dynamic Media]

   * 选择性发布 — 营销团队现在可以访问 [!DNL Dynamic Media] 智能裁剪图像和动态演绎版已同步到 [!DNL Dynamic Media] 这样他们就可以制作宣传材料，而无需将这些资产发布到 [!DNL Dynamic Media] 用于全球交付。 [!DNL Experience Manager] 和 [!DNL Dynamic Media] 发布是相互分离的，可单独进行以实现此目的。 请参阅 [选择性发布](/help/assets/dynamic-media/selective-publishing.md).
   * 管理员现在可以重置 [!DNL Dynamic Media] Cloud Service预配时收到的密码。 可在中完成重置 [!DNL Experience Manager] 用户界面，无需使用 [!DNL Dynamic Media Classic] 桌面应用程序。

* 要了解以下增强功能，请参阅 [Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Adobe Document Cloud视图SDK集成增强了PDF预览。
   * 单击下载功能。
   * 下载体验的新管理配置。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF核心组件v1.3.0。请参阅 [CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 以了解更多详细信息。

* 现在提供了产品和类别模板的产品/类别预览功能。 这允许AEM中的业务用户/营销人员查看包含真实数据的产品/类别模板。

* 产品和类别中添加了属性页面，以允许业务用户查看与产品SKU/类别id关联的详细信息。

* 产品控制台中添加了排序功能，以允许按名称或价格属性对产品/类别进行排序。

* 产品搜索功能已添加到产品控制台。

### 错误修复 {#bug-fixes-commerce}

* Commerce Cloud配置不遵循继承。 已修复此问题，以确保配置继承值。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

的发行日期 [!UICONTROL Cloud Manager] 2020.9.0版是2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核已重新标记为体验审核。
* 构建过程已分为三个单独的Maven命令。
* 如果Git存储库克隆失败，则最多将重试三次。

### 错误修复 {#bug-fixes-cm}

* “内容审核”选项卡使用创作域而不是发布域错误地显示了基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

请阅读本章内容，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* 云就绪分析器(CRA)有一个开始状态控制台，该控制台显示一个明确的 **生成报表** 按钮，以执行CRA。

* CRA UI在运行时会显示进度。 它显示正在分析的项目以及在执行过程中找到的结果。

* CRA报告以表格形式显示了调查结果的摘要和数量，按调查结果类型和重要性级别进行组织。 单击该发现结果的编号将自动滚动到该发现结果在报表中的位置。

### 错误修复 {#cra-bug-fixes}

* 在某些情况下，强制刷新后，CRA报告未更新。 此版本已修复此问题。

## 内容转移工具 {#content-transfer-tool}

请阅读本节内容，了解内容传输工具版本v1.1.10的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)支持Azure Blob Store数据存储。

* CTT用户界面具有自动重新加载功能，每30秒重新加载一次概述页面。

* 添加到CTT用户界面以检索的按钮 *访问令牌* 容易。

* 添加了描述性验证消息 *URL* 和 *迁移集名称*.

## 代码重构工具 {#code-refactoring}

请阅读本节内容，了解代码重构工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI插件支持Repository Modernizer，并允许用户使用插件执行该工具。

   请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 以了解更多详细信息。

* Repository Modernizer实用程序可用于将现有项目包重构为与为AEMas a Cloud Service定义的项目结构兼容的包。

   请参阅 [Git资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以了解更多详细信息。
