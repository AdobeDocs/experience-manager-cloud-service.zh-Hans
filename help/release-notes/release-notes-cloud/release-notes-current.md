---
title: Adobe Experience Manager 云服务 2020.7.0 发行说明
description: Experience Manager 2020.7.0 发行说明
translation-type: tm+mt
source-git-commit: 610e00a8669a7d81482d99685d200bd705b1848f
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 18%

---


# AEM 云服务 2020.7.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.7.0 的常规发行说明。

## Cloud Manager 的新增功能 {#cloud-manager}

阅读本节内容，了解 AEM 云服务版本 2020.7.0 中 Cloud Manager 的新增功能和更新。

### 发布日期 {#release-date}

Cloud Manager Version 2020  .7.0的发布日期为2020年7月9日。

### 新增功能 {#what-is-new-cloud-manager}

* 环境页面已重新设计。

* 冬眠环境在冬眠后，现在在Cloud Manager中显示离散状态。

* 每个环境的环境变量数已增加到200个。

* Cloud Manager构建容器现在支持Java 8和Java 11。

### 错误修复 {#bug-fixes-cm}

* 在完全创建环境之前，从云管理器到开发人员控制台的链接未正确激活。

* 直接从云管理器链接到开发人员控制台时，未显示用于将沙箱项目的环境解除休眠／休眠的选项。

* “非 **生** 产管道 **** ”编辑页面上的“取消”和“保存”选项并不总是可见。

* 代码质量过程中的某些失败可能导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回现有项目名称的重复。

* 无法通过用户界面一致地下载某些大型管道步骤日志。

* 验证环境名称时出现非按一错误。

* 环境页有时会显示发布和调度程序段（当不存在时）。

### 已知问题 {#known-issues}

* 由于代码覆盖率的计算方式发生 _更改_ ,Jacoco插件的最低版本现在为0.7.5.201505241946（发布于2015年5月）。 明确引用旧版本的客户将在代码质量过程中收到错误消息。

## 云就绪性分析器的新增功能 {#cloud-readiness-analyzer}

可查看本节以了解新增功能以及Cloud Readiness Analyzer Release 1.0.2版的更新。

### 错误修复 {#cra-bug-fixes}

* 无法在Adobe Experience Manager(AEM)6.1上运行CRA的早期版本。添加了允许管理员组中用户的明确支持。

   有关详 [细信息，请参阅在AEM 6.1上安装](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) CRA。

* 摘要报告上显示的过期时间戳不正确。

* CRA正在检测重复的定制组件。

* 在AEM 6.1上，内容检查在完成完整检查之前已退出。 添加了异常处理，以允许检查员跳过并继续，直到完成完整检查。

