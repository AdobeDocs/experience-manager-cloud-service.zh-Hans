---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.8.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.8.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 99772a1a3faa454a9b07dd92c9e7622ddb37ce2d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 24%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.8.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.8.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 2023.8.0 中的 Cloud Manager 的发布日期是 2023 年 8 月 10 日。 下一个版本计划于 2023 年 7 月 9 日发布。

## 新增功能 {#what-is-new}

* 配置内容集时 [复制内容，](/help/implementing/developing/tools/content-copy.md) [上下文感知配置](/help/implementing/developing/introduction/configurations.md) 现在允许在UI的内容集中使用。
* 增强了以提高Cloud Manager UI中错误消息的可理解性和显示性。

## 提前采用计划 {#early-adoption}

加入我们的早期采用计划，并有机会测试即将推出的某些功能。

### 自助内容恢复 {#content-restore}

[新的自助内容恢复功能](/help/operations/restore.md) 现在提供长达7天的备份恢复，供早期采用者用于评估，其特点是：

* 过去24小时的时间点备份恢复
* 固定时间恢复最长可达7天

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `aemcs-restorefrombackup-adopter@adobe.com` 来自与Adobe ID关联的电子邮件。 请注意：

* 早期采用者计划仅适用于开发环境。
* 此功能早期采用者计划的可用性有限。
* 此功能用于恢复意外删除的内容，而不是用于灾难恢复。

### 体验审核功能板 {#experience-audit-dashboard}

[Cloud Manager体验审核功能板](/help/implementing/cloud-manager/experience-audit-dashboard.md) 包括您的页面性能分数的趋势视图，以及可帮助您改进这些分数的见解和推荐。 体验审核作为Cloud Manager生产管道中的步骤包括在内。

功能板利用Google Lighthouse（一种开源自动工具）来提高Web应用程序的质量。 您可以针对任何网页（公共网页或需要身份验证的网页）运行它。 它审核性能、可访问性、渐进式Web应用程序、SEO等。

有兴趣试驾新仪表板？ 请发送电子邮件至 `aem-lighthouse-pilot@adobe.com` 从与Adobe ID关联的电子邮件中，我们可以帮助您入门。

## 错误修复 {#bug-fixes}

* 此 **环境** 现在，菜单在触发 **[复制内容](/help/implementing/developing/tools/content-copy.md)** 模式。
* [管道重新执行](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) 如果上一个执行没有 `commitId` 在构建阶段状态上设置。
* 现在，当用户单击中的管道时，会显示一条更易于理解的消息，指出罕见的错误 **活动** 或 **管道** 屏幕。
* 此 `contentSetName` 值在日志中不再缺失，现在，在开始 [内容复制](/help/implementing/developing/tools/content-copy.md) 操作。
* 在某些极少数情况下，不再可能从同一管道开始两次执行，从而导致“卡住”状态。
* 证书过期后，与证书关联的域名和IP允许列表将不再从CDN中删除。
   * 在此类情况下，该站点可继续访问。
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)Cloud Manager UI 将显示更多醒目的事先警告，强调 SSL 证书即将到期。
* 修复了将Sites作为解决方案添加到仅限Assets程序时，AEM无法访问发布端点的问题。
