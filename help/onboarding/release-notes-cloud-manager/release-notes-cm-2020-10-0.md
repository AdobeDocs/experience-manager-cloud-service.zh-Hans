---
title: 2020.10.0 版发行说明
description: 2020.10.0 版发行说明
translation-type: tm+mt
source-git-commit: 9ed52fb3a9971bcaede71613774f653273a86530
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 60%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

本页概述了AEM中作为Cloud Service2020.10.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service2020.10.0的发布日期为2020年10月1日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 环境页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* Cloud Manager 内部版本容器现在同时支持 Java 8 和 Java 11。

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