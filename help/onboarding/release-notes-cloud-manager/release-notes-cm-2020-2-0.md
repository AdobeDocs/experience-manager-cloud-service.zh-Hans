---
title: AEM as a Cloud Manager版本2020.2.0的发行说明
description: AEM as a Cloud Manager版本2020.2.0的发行说明
feature: 发行信息
exl-id: 3f3324d9-53db-458d-9523-2e0d5d6dc3f7
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 67%

---

# Adobe Experience Manager as a Cloud Service2020.2.0 {#release-notes}中的Cloud Manager发行说明

本页面概述了AEM as a Cloud 2020.2.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service2020.2.0中的Cloud Manager的发布日期是2020年2月13日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Adobe Experience Manager 原型版本已更新至版本 22。
* 现在，可以通过 Cloud Manager UI 来更新沙盒/演示程序中的暂存环境和生产环境。
* 优化了 Experience Cloud 通知中使用的 URL，以避免多余的重定向。
* 现在，超时的管道执行步骤会明确地指出这一点。
* 现在，“代码扫描”步骤有可下载的日志。
* 现在，包含代码扫描过程所发现问题的电子表格有这样一列：该列包含指向特定规则文档的链接。

### 错误修复 {#bug-fixes}

* 有时，浏览器安全策略会妨碍管道执行屏幕中的某些按钮正常工作。
* 有时，Cloud Manager 登陆页面上会提供“概述”、“环境”和“活动”链接。
* 部署时的某些故障，可能会错误地阻止新管道的创建。
