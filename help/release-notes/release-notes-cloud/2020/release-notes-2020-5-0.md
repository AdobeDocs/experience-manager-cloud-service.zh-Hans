---
title: Adobe Experience Manager as a Cloud Service 2020.5.0 发行说明
description: Experience Manager 2020.5.0 发行说明
exl-id: 8570d2c3-6d55-4914-94b2-f5d162e0c285
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 100%

---

# AEM as a Cloud Service 2020.5.0 发行说明 {#release-notes}

本页面概述了 Experience Manager as a Cloud Service 2020.5.0 版的常规发行说明。

## 发布日期 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.5.0 的发布日期是 2020 年 5 月 7 日。

## AEM Sites 的新增功能 {#aem-sites}

阅读本节内容，了解 AEM as a Cloud Service 版本 2020.5.0 中 AEM Sites 的新增功能和更新。

* 现在，将批量页面移动和转出作为异步作业处理后，可以获得详细的作业信息。
* 复制/粘贴页面树时，现在可以选择仅粘贴树的根页面，或者同时粘贴树的子页面。
* 现在，导出到 Adobe Target 工作区的 AEM 体验片段在 Target 中显示为唯一的选件类型和选件源。
* MSM - 现在，使用“发布”**&#x200B;触发器可成功转出 Live Copy 源中组件的删除事件，即在 Live Copy 中删除 Live Copy 源中已删除的组件。
* MSM - 现在，从 Live Copy 源中转出组件后，Live Copy 中的相同组件会重命名为 *_msm_moved*。


## Cloud Manager 的新增功能 {#cloud-manager}

阅读本节内容，了解 AEM as a Cloud Service 版本 2020.5.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new}

* 添加了六个其他代码质量规则，以帮助客户在计划迁移到云服务时发现潜在问题。
* 添加了一个新量度“云服务兼容性”**，以汇总与兼容性相关的问题数量。
* 现在，创建失败的环境将在创建失败后大约 24 小时自动删除，除非已删除这些环境。
* “活动”页面和管道执行列表 API 的性能已得到改进。
* 代码质量日志现在包含完整的异常堆栈追踪。

### 错误修复  {#bug-fixes}

* 生产管道运行时，概述页面上显示误导性信息卡。
* *DontImplementOrExtendProviderTypesPomCheck* 代码质量规则有时可能会产生“空指针异常”。
* 概述页面中的某些文档链接无法正常使用。
* “创建环境”对话框在 Safari 中无法正确呈现。
* 概述页面上的某些信息卡无法正确显示实体名称。
* 在某些情况下，“生成图像”可能无法成功下载客户包。
