---
title: AEM as a Cloud Manager版本2020.7.0的发行说明
description: AEM as a Cloud Manager版本2020.7.0的发行说明
feature: 版本信息
exl-id: b5ac4dd4-18c6-4867-b2df-53711555007f
source-git-commit: 596a7a41dac617e2fb57ba2e4891a2b4dce31fad
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 73%

---

# Adobe Experience Manager as a Cloud 2020.7.0版中的Cloud Manager发行说明 {#release-notes}

本页面概述了AEM as a Cloud 2020.7.0中的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Manager 2020.7.0Cloud Service中Cloud Manager的发布日期是2020年7月9日。

## 新增功能 {#whats-new-cloud-manager}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* 每个环境的环境变量数量已增加至 200 个。

* Cloud Manager 管道现在支持由客户设置的变量和密钥。


   有关更多详细信息，请参阅管道变量。

* 现在支持绑定身份验证的专用Maven存储库。

* Cloud Manager 内部版本容器现在同时支持 Java 8 和 Java 11。有关更多详细信息，请参阅使用Java 11支持。

### 错误修复 {#bug-fixes-cm}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的&#x200B;**取消**&#x200B;和&#x200B;**保存**&#x200B;选项并非一直可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。

### 已知问题 {#known-issues}

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;*最低*&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户将会在代码质量控制过程中收到一条错误消息。
