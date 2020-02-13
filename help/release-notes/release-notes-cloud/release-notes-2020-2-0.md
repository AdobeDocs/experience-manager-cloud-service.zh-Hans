---
title: 2020.2.0版发行说明
description: 2020.2.0版发行说明
translation-type: tm+mt
source-git-commit: 157809fb4aacf45358db6412dea04398a7f12495

---


# AEM作为云服务的发行说明2020.2.0 {#release-notes}

以下部分概述了Experience manager作为云服务2020.2.0的一般发行说明。

发布日期为2020年2月13日。

## Cloud Manager {#cloud-manager}

可查看本节以了解Cloud Manager 2020.2.0版的新增功能和更新。

### 新增功能 {#what-is-new}

* Adobe Experience manager原型版本已更新至版本22。
* 沙箱／演示程序中的舞台和生产环境现在可以通过Cloud Manager UI更新。
* Experience cloud通知中使用的URL已优化，以避免额外重定向。
* 现在超时的管道执行步骤显式声明此。
* “代码扫描”步骤现在有可下载的日志。
* 现在，包含在代码扫描过程中发现的问题的电子表格有一列，其中包含指向特定规则文档的链接。

### 错误修复 {#bug-fixes}

* 浏览器安全策略有时会阻止管道执行屏幕中的某些按钮正常工作。
* “概述”、“环境”和“活动”链接有时可在Cloud manager登录页面上使用。
* 部署时的某些故障可能会错误地阻止创建新管线。