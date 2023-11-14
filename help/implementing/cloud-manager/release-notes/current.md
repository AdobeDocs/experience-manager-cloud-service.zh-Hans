---
title: Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2023.11.0 发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.11.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b51b3c9aed4d9dacbf12a6cad5f8923d82766bd9
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 53%

---


# Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2023.11.0 发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.11.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.11.0 的发布日期是 2023 年 11 月 14 日。下一个版本计划于2023年12月7日发布。

## 新增功能 {#what-is-new}

* Web应用程序防火墙 — DDOS保护(WAF-DDOS)现在可作为您的AEMas a Cloud Service权利的一部分购买，并且 [可以自助方式配置。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* 专业化 [配置部署管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 管道现在可用于在几分钟内配置环境设置、维护任务、CDN规则等。
* [复制内容时](/help/implementing/developing/tools/content-copy.md) 从更高的环境到开发环境，现在会显示一条消息，建议在复制大型内容集时务必谨慎，因为开发环境存在容量限制。
* [管道执行详细信息页面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 现在将显示管道执行中的所有步骤，其中尚未开始的步骤将显示为灰色。
* 在两者上 **[活动](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** 和 **[管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** 现在，在单击处于运行状态的管道时，会显示管道执行摘要。
* 新 **持续时间** 部分已添加到 [管道详细信息页面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 这包括基于该项目历史趋势的管道步骤的平均持续时间。
* 在管道执行页面上，完成的步骤现在显示持续时间。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能。

### 自带GitHub {#byo-github}

如果您使用GitHub管理存储库， [您现在可以通过Cloud Manager直接在GitHub存储库中验证代码。](/help/implementing/cloud-manager/managing-code/byo-github.md) 此集成消除了对代码与Adobe存储库保持一致同步的需求，并允许您在将拉取请求合并到主分支之前对其进行验证。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com` 从与Adobe ID关联的电子邮件地址中查找。

### 自定义权限 {#custom-permissions}

[Cloud Manager 自定义权限](/help/implementing/cloud-manager/custom-permissions.md)可让您创建具有可配置权限的新的自定义权限配置文件，以限制 Cloud Manager 用户对项目、管道和环境的访问。

如果您有兴趣测试此新功能并共享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager-custom-permissions@adobe.com`。

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

## 已知问题 {#known-issues}

存在一个已知的错误阻止 [配置部署管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) 被推送到生产环境中。

如果 **在部署到生产环境之前暂停** 配置部署管道需要选项，在解决错误之前，建议使用以下解决方法。

1. 运行管道.
1. 在暂存环境中测试代码。
1. 当部署和批准变得可用时，单击 **拒绝**.
1. 编辑管道以禁用 **在部署到生产环境之前暂停** 选项。
1. 再次运行管道。 它将在暂存环境中再次运行，然后在生产环境中再次运行。
