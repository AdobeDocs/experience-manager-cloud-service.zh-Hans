---
title: AEMas a Cloud Service版本2020.10.0中的Cloud Manager发行说明
description: AEMas a Cloud Service版本2020.10.0中的Cloud Manager发行说明
feature: Release Information
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 48%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2020.10.0 {#release-notes}

本页概述了AEM as a Cloud Service 2020.10.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager的发行日期为2020.10.0 2020年10月1日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager内部版本容器现在支持使用Java 8或Java 11编译项目。 Maven工具链系统提供对Java 11的支持。

* 每个环境的环境变量数量已增加至 200 个。

* “概述”页面上的“环境”卡现在最多将列出三个环境。 用户可以选择 **显示全部** 按钮以导航到“环境摘要”页以查看包含环境完整列表的表。
请参阅 [查看环境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 以了解更多详细信息。


### 错误修复 {#bug-fixes-cloud-manager}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的取消和保存按钮并不总是可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。
