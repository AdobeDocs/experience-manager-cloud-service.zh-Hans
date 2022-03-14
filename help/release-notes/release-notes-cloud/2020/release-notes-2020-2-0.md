---
title: 2020.2.0 版发行说明
description: 2020.2.0 版发行说明
exl-id: 005c4756-44c6-4af5-9b0c-0fc07bd211a0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# AEM as a Cloud Service 2020.2.0 发行说明 {#release-notes}

本页面概述了 Experience Manager as a Cloud Service 2020.2.0 版的常规发行说明。

## 发布日期 {#release-date}

Experience Manager as a Cloud Service 2020.2.0 的发布日期是 2020 年 2 月 13 日。

## Cloud Manager {#cloud-manager}

阅读本节内容，了解 AEM as a Cloud Service 版本 2020.2.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new}

* Adobe Experience Manager 原型版本已更新至版本 22。
* 现在，可以通过 Cloud Manager UI 来更新沙盒/演示程序中的暂存环境和生产环境。
* 优化了 Experience Cloud 通知中使用的 URL，以避免多余的重定向。
* 现在，超时的管道执行步骤会明确地指出这一点。
* 现在，“代码扫描”步骤有可下载的日志。
* 现在，包含代码扫描过程所发现问题的电子表格有这样一列：该列包含指向特定规则文档的链接。

### 错误修复  {#bug-fixes}

* 有时，浏览器安全策略会妨碍管道执行屏幕中的某些按钮正常工作。
* 有时，Cloud Manager 登陆页面上会提供“概述”、“环境”和“活动”链接。
* 部署时的某些故障，可能会错误地阻止新管道的创建。
