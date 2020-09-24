---
title: ' [!DNL Adobe Experience Manager]  云服务 2020.9.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明。'
translation-type: tm+mt
source-git-commit: f39b03455fc03104932952b892b88403d0c9eca7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 15%

---


# [!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.9.0 版的常规发行说明。

## 发布日期 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 is September 24, 2020.

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* 单页应用程序(SPA)编辑器JavaScript SDK现 [在是开放源码。](/help/implementing/developing/spa/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* 使用资产微服务生成的演绎版支持为PNG图像添加水印。 它可以配置为处理用户档案。

* 中的增强功能 [!DNL Dynamic Media]

   * 选择性发布——营销团队现在可以访问同步到的 [!DNL Dynamic Media] 智能裁剪图像和动态演绎版，以便 [!DNL Dynamic Media] 创建促销资料，而无需将这些资产发布到全局 [!DNL Dynamic Media] 投放。 AEM和 [!DNL Dynamic Media] 发布是相互分离的，可单独执行，以实现这一点。
   * 管理员可以 [!DNL Dynamic Media] 直接在AEM UI中重置设置时收到的Cloud Service口令，而无需使用桌面 [!DNL Dynamic Media Classic] 应用程序。

* 要了解以下增强功能，请 [参阅Brand Portal的新增功能](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/introduction/whats-new.html)。

   * 集成Adobe Document Cloud视图SDK，增强PDF预览。
   * 单击下载功能。
   * 下载体验的新管理配置。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF核心组件v1.3.0。有关更多详 [细信息，请参阅](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) CIF核心组件。

* 产品/预览模板的类别功能和类别模板现已可用。 这使AEM的商业用户／营销人员能够视图产品/类别模板和真实数据。

* 属性页面已添加到产品和类别中，以允许业务用户视图与产品SKU/类别id关联的详细信息。

* 添加到产品控制台的排序功能允许按名称或价格属性对产品/类别进行排序。

* 产品搜索功能已添加到产品控制台。

### 错误修复 {#bug-fixes-commerce}

* Commerce Cloud配置不尊重继承。 已对此进行修复，以确保配置继承值。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核已重新标记为体验审核。
* 构建过程已分为三个单独的Maven命令。
* 如果无法克隆Git存储库，则最多将重新尝试三次。

### 错误修复 {#bug-fixes-cm}

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

请阅读本章内容，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* 云就绪性分析器(CRA)具有开始状态控制台，该控制台显 **示用户单击** “生成报告”按钮以执行CRA。

* CRA UI在运行时显示进度。 它显示正在分析的项目和在执行过程中找到的结果。

* CRA报告以表格形式显示了调查结果的摘要和数量，按调查结果类型和重要性级别进行组织。 单击该查找结果的数量将自动滚动到该查找结果在报告中的位置。

### 错误修复 {#cra-bug-fixes}

* 在某些情况下，强制更新后，CRA报告没有得到更新。 此版本中已修复此问题。

## 内容传输工具 {#content-transfer-tool}

可查看本节以了解新增功能以及内容传输工具版本1.1.10的更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)支持Azure Blob存储数据存储。

* CTT用户界面具有自动重新加载功能，每30秒重新加载一次概述页面。

* 添加到CTT用户界面的按钮可轻松 *检索访问令牌* 。

* 为URL和迁移集名称 *添加**了描述性验证消息*。
