---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.4.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.4.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: f1d8778f3cfb6868740141d008fd0217839e9103
workflow-type: ht
source-wordcount: '706'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.4.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.4.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.4.0 版本的发布日期是 2024 年 4 月 10 日。下一个版本计划于 2024 年 5 月 9 日发布。

## 新增功能 {#what-is-new}

* 通过更新与 [Edge Delivery](/help/edge/overview.md) 网站相关的程序中的域映射，改进了对该网站的删除操作。
   * 如果不再映射站点，则会删除映射。
* 通过在 AEM 实例的关键启动阶段提供实时状态更新，增强了部署跟踪功能。
   * 此功能可以确保您完全了解部署进度，从而做出更好的决策并提高运营效率。
* [网络基础设施](/help/security/configuring-advanced-networking.md)列表经过增强，可以显示所有连接的环境，而无需基于区域而进行筛选，从而提供更全面的视图。
* 增强的代码构建问题错误消息可以更轻松地识别根本原因和下一步可操作的步骤。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### 通过真实用户监控 (RUM) 进行客户端收集 {#rum}

您可以利用[真实用户监控 (RUM) 数据服务](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)为 AEM as a Cloud Service 启用客户端收集。

真实用户监控 (RUM) 数据服务能够更准确地反映用户交互，确保可靠地衡量网站参与度。这是一个深入了解页面性能的绝佳机会。这对于使用 Adobe 管理的 CDN 或非 Adobe 管理的 CDN 的客户都很有用。对于使用非 Adobe 管理的 CDN 的客户，现在可为其启用自动流量报告，这样即无需与 Adobe 共享任何流量报告。

如果您有兴趣测试这项新功能并共享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址向 `aemcs-rum-adopter@adobe.com` 发送一封电子邮件。请在您的电子邮件中包含生产、暂存和开发环境的域名。参与此功能的早期采用者计划的人数受限。

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/implementing/cloud-manager/managing-code/byo-github.md)此集成使得无需始终与 Adobe 存储库同步代码，并使您可验证拉取请求后再将其合并到主分支中。此功能为公共 GitHub 所独有。不支持自托管的 GitHub。

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。

### 自助内容恢复 {#content-restore}

[新的自助内容恢复功能](/help/operations/restore.md)现在提供长达 7 天的备份恢复，并可供早期采用者用于评估目的，其中包括：

* 前 24 小时的时间点备份恢复
* 固定时间恢复最长可达 7 天

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件发送电子邮件至 `aemcs-restorefrombackup-adopter@adobe.com`。

* 早期采用者计划仅限于开发环境。
* 参与此功能的早期采用者计划的人数受限。
* 此功能用于恢复意外删除的内容，不适用于灾难恢复。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？若要开始使用，请从与您的 Adobe ID 关联的电子邮件发送电子邮件至 `aem-lighthouse-pilot@adobe.com`。

## 错误修复 {#bug-fixes}

* 解决了 Cloud Manager 重复使用具有错误提交哈希的工件的错误。
