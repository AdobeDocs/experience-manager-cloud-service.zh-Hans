---
title: ' [!DNL Adobe Experience Manager]  云服务 2020.9.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明。'
translation-type: tm+mt
source-git-commit: a2037fb3a315db801423c33671e1885a0b655391
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 22%

---


# [!DNL Adobe Experience Manager] 云服务 2020.9.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.9.0 版的常规发行说明。

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
