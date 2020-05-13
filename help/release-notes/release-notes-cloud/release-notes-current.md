---
title: Adobe Experience Manager 云服务 2020.5.0 发行说明
description: Experience Manager 2020.5.0 发行说明
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# AEM 云服务 2020.5.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.5.0 的常规发行说明。

## Cloud Manager {#cloud-manager}

阅读本节内容，了解 AEM 云服务版本 2020.5.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new}

* 新增了六条代码质量规则，帮助客户在规划迁移到云服务时发现潜在问题。
* 新增了一 *个度量云服务兼容性* ，以总结与兼容性相关的问题数。
* 未能创建的环境现在将在创建失败后约24小时自动删除，除非已删除它们。
* 活动页面和管道执行列表API的性能已得到改进。
* 代码质量日志现在包含完整的堆栈跟踪以发现异常。

### 错误修复 {#bug-fixes}

* 在生产管道运行时，概述页面上会显示误导性信息卡。
* DontImplementOrExtendProviderTypesPomCheck代码质量 *规则有时可能* 会产生空指针异常。
* 概述页面中的某些文档链接无法正常工作。
* 创建环境对话框在Safari中无法正确呈现。
* 概述页面上的某些卡未正确显示实体名称。
* 在某些情况下，构建映像无法成功下载客户包。

