---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 6ca376bda8055d62e35e13053ff21f861c12b292
workflow-type: ht
source-wordcount: '548'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.6.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.6.0 版本的发布日期是 2024 年 6 月 6 日。下一个版本计划于 2024 年 7 月 18 日发布。

## 新增功能 {#what-is-new}

* 您现在可以[使用您自己的 GitHub 存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)作为全堆叠和前端管道的源。
   * 此外，您还可以利用带有 [Git 子模块](/help/implementing/cloud-manager/managing-code/git-submodules.md)的 GitHub 存储库，为您提供对用于拉取请求验证的自动生成管道的增强控制，并允许您在代码扫描阶段定义关键指标的行为。
   * [您还可以选择](/help/implementing/cloud-manager/managing-code/github-check-config.md) 在 GitHub 上保存报告历史记录、命名管道和设置管道变量以满足您的需求。
* [自助内容恢复](/help/operations/restore.md)提供长达七天的备份恢复功能，并具有以下特点：
   * 前 24 小时的时间点备份恢复
   * 固定时间恢复最长可达 7 天
* [新的 OakPal 规则](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package)已添加到 Cloud Manager 代码质量扫描中。
   * 自 2024 年 6 月起添加的每条新规则都是非重大更改。
   * 我们建议您尽快解决这些问题，因为从 Cloud Manager 2024 年 8 月版本开始，这些新规则将导致管道失败。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### Cloud Manager 中的 Edge Delivery Services 支持 {#edge-delivery-services}

如果您已将 Edge Delivery Services 作为 Adobe Experience Manager Sites 的一部分进行了许可，[您现在可以直接在 Cloud Manager 中使用 Edge Delivery Services 登录您的网站](/help/implementing/cloud-manager/edge-delivery-services.md)，并使用引导式自助服务体验上线。

这可为您的所有 AEM 属性提供统一的体验，确保与所有重要工作流（包括域名管理、SSL 证书管理和 CDN 映射）协调一致。

如果您有兴趣测试这项新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向 `aemcs-cmedgedelsvs-program-adopter@adobe.com` 发送一封电子邮件。

### 域验证 (DV) 证书

Cloud Manager 现在允许您[自助生成和管理域验证 (DV) SSL 证书。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 这可为您提供最快捷、最简单、最具成本效益的解决方案，从而为您的在线业务创建一个安全的网站。

如果您有兴趣测试这项新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向 `Grp-aemcs-dv-dert-adopter@adobe.com` 发送一封电子邮件。

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited.-->

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？若要开始使用，请从与您的 Adobe ID 关联的电子邮件发送电子邮件至 `aem-lighthouse-pilot@adobe.com`。
