---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.10.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.10.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 661eac787439e6e696574a6973afa7e39eeb443e
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 62%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.10.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.10.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 2023.10.0 版本中的 Cloud Manager 的发布日期是 2023 年 10 月 5 日。 下一个版本计划于 2023 年 11 月 2 日发布。

## 新增功能 {#what-is-new}

* [您现在可以安全地取消管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#cancel) 在验证和构建图像步骤中。
* 改进了 [索引](/help/operations/indexing.md) 缩短了部署新索引时的管道持续时间。
   * 改进功能因内容配置文件而异。
* 自动 [更新了开发环境](/help/implementing/cloud-manager/manage-environments.md#updating-environments) 默认情况下，新程序将启用，从而节省手动执行更新的时间。
   * 此更新将分阶段推出。
* 在2023年10月版的Cloud Manager中，将通过分阶段推出来更新Java和Maven版本。
   * 正在将Apache Maven更新到版本3.8.8。
   * Java版本正在更新以OracleJDK 8u371和OracleJDK 11.0.20。
   * 默认情况下， `JAVA_HOME` 正在将环境变量更新到 `/usr/lib/jvm/jdk1.8.0_371` 其中包含OracleJDK 8u371。
   * 查看文档 [构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 以了解更多详细信息。
   * [请参阅OpenJDK建议](https://openjdk.org/groups/vulnerability/advisories/) 有关这些JDK更新中的安全和错误修复的详细信息。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能。

### 自定义权限 {#custom-permissions}

[Cloud Manager自定义权限](/help/implementing/cloud-manager/custom-permissions.md) 允许您创建新的自定义权限配置文件，可配置权限以限制对Cloud Manager用户的项目、管道和环境的访问。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `Grp-CloudManager-custom-permissions@adobe.com` 从与Adobe ID关联的电子邮件地址中查找。

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
