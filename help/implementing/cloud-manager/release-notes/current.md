---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.8.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2024.8.0 发行说明。
feature: Release Information
role: Admin
source-git-commit: a823bcd1461b847983d0243cd9abd59efd8d7b6f
workflow-type: ht
source-wordcount: '465'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2024.8.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.8.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.8.0 版本的发布日期是 2024 年 8 月 14 日。下一个版本计划于 2024 年 9 月 14 日发布。

## 新增功能 {#what-is-new}

* 现在，AEM Forms as a Cloud Service 可提供[额外的发布区域](/help/operations/additional-publish-regions.md) 和 [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)（服务级别协议）。
   * 通过此增强功能，您可以实现更高的 SLA、更长的正常运行时间和更低的延迟，从而确保为全球分布的用户提供一流的体验。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### Cloud Manager 中的 Edge Delivery Services 支持 {#edge-delivery-services}

如果您已将 Edge Delivery Services 作为 AEM Sites 的一部分获得许可，[您现在就可以直接在 Cloud Manager 中使用 Edge Delivery Services 登录您的网站](/help/implementing/cloud-manager/edge-delivery-services.md)，并使用引导式自助服务体验上线。

此功能为您的所有 AEM 属性提供了统一的体验。它确保域名管理、SSL 证书管理和 CDN 映射等关键工作流程的一致性。

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `aemcs-cmedgedelsvs-program-adopter@adobe.com`。

### 域验证（DV）证书

借助 Cloud Manager，您现在可以[自助生成和管理域验证 (DV) SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)。此功能为您提供最快捷、最简单、最具成本效益的解决方案，为您的在线业务创建一个安全的网站。

如果您想测试此新功能并提供反馈，请使用与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-aemcs-dv-dert-adopter@adobe.com`。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以使用它来审核任何网页，无论是公开的还是需要身份验证的。它提供对性能、可访问性、渐进式 Web 应用程序、SEO 等的评估。

想要尝试新的仪表板吗？首先，使用与您的 Adobe ID 关联的电子邮件向 `aem-lighthouse-pilot@adobe.com` 发送电子邮件。

## 错误修复

* 纠正了一个罕见的问题，即在删除管道后发现管道步骤仍在运行。
* 修复了配置管道在极少数情况下错误显示 `FAILED` 状态的问题。
