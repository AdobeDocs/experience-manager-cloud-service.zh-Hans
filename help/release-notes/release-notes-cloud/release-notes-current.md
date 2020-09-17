---
title: ' [!DNL Adobe Experience Manager]  云服务 2020.9.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明。'
translation-type: tm+mt
source-git-commit: 9bb087cb0570a1f3bbffb989a9399d3274f9c5e1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 20%

---


# [!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.9.0 版的常规发行说明。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* 单页应用程序(SPA)编辑器Javascript SDK现 [在是开放源码。](/help/implementing/developing/spa/reference-materials.md)

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

