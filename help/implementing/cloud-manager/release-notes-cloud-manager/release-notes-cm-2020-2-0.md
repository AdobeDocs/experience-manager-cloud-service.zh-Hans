---
title: AEM 2020.2.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2020.2.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
exl-id: 3f3324d9-53db-458d-9523-2e0d5d6dc3f7
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 66%

---

# Adobe Experience Manager as a Cloud Service 2020.2.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2020.2.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2020.2.0版中Cloud Manager的发布日期是2020年2月13日。

## Cloud Manager {#cloud-manager}

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
