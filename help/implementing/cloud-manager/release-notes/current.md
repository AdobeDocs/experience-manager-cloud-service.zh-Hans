---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.9.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.9.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 8bf2ffe8b1d3780f4ad3f6972fea4f8281945abb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 76%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.9.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.9.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.9.0 的发布日期是 2023 年 9 月 14 日。 下一个版本计划于 2023 年 10 月 5 日发布。

## 新增功能 {#what-is-new}

* CDN日志（如果可用）可通过Cloud Manager UI下载。
* 用户现在可以选择加入由Google Lighthouse提供支持的Experience Audit测试，并将其包含在非生产全栈管道中。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能。

### 自助内容恢复 {#content-restore}

[新的自助内容恢复功能](/help/operations/restore.md)现在提供长达 7 天的备份恢复，并可供早期采用者用于评估目的，其中包括：

* 前 24 小时的时间点备份恢复
* 固定时间恢复最长可达 7 天

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件发送电子邮件至`aemcs-restorefrombackup-adopter@adobe.com`。请注意：

* 早期采用者计划仅限于开发环境。
* 此功能的早期采用者计划的可用性是有限的。
* 此功能用于恢复意外删除的内容，不适用于灾难恢复。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？请从与您的 Adobe ID 关联的电子邮件发送电子邮件至`aem-lighthouse-pilot@adobe.com`，我们可以帮助您开始。

## 错误修复 {#bug-fixes}

* 删除程序时，还将删除任何关联的正在运行的管道，确保不会将管道错误地指定为失败状态。
* 上线完成按钮被禁用，并通知用户管道正在进行的原因。
* 有时，当管道执行的所有步骤都是“已完成”时，管道的状态会视为“正在运行”，使其似乎处于卡住状态。 它现在被视为“完成”。
