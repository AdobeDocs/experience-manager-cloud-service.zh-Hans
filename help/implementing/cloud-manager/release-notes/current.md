---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: a5cd55bcdc6044dd8db26f009b955216cda5daee
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 60%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.7.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.7.0版的发布日期为2024年7月18日。 计划于 2024 年 8 月 8 日发布下一个版本。

## 新增功能 {#what-is-new}

* [生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)和[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)在Git更改上触发&#x200B;**On Git Changes**&#x200B;以在提交上启动管道，现在可供[专用存储库使用。](/help/implementing/cloud-manager/managing-code/private-repositories.md)
   * 将分阶段推出，并在8月中旬之前完成。
* 添加[Adobe管理的DV证书](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)时，您现在可以添加单个涵盖多个域的证书，而不是为每个域创建证书。
* 现在可以将没有[其他发布区域](/help/operations/additional-publish-regions.md)的解决方案添加到程序中，前提是该程序至少具有Sites或Forms解决方案适用于该程序。
* 现在可以将不具有[99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)的解决方案添加到程序，只要该程序至少具有Sites或Forms解决方案适用于该程序。
* [体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)已增强多种方式。
   * 审核现在通过CDN针对`.com`端点运行，取代了以前的`.net`方法。
      * 此更改更准确地模拟真实的用户体验，并帮助您在管理和优化网站方面做出更明智的决策。
   * 对体验审核UI进行了多项增强，包括：
      * 添加了性能、最佳实践、SEO和可访问性的趋势视图。
      * Lighthouse原始报表链接现在以更直观的方式显示，直接显示在扫描快照详细信息面板中。
      * Lighthouse推荐部分已得到增强。
   * 根据Lighthouse版本12.0.0删除了PWA指标，从而消除了该指标。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### Cloud Manager 中的 Edge Delivery Services 支持 {#edge-delivery-services}

如果您已将 Edge Delivery Services 作为 Adobe Experience Manager Sites 的一部分进行了许可，[您现在可以直接在 Cloud Manager 中使用 Edge Delivery Services 登录您的网站](/help/implementing/cloud-manager/edge-delivery-services.md)，并使用引导式自助服务体验上线。

这可为您的所有 AEM 属性提供统一的体验，确保与所有重要工作流（包括域名管理、SSL 证书管理和 CDN 映射）协调一致。

如果您有兴趣测试这项新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向 `aemcs-cmedgedelsvs-program-adopter@adobe.com` 发送一封电子邮件。

### 域验证 (DV) 证书

Cloud Manager 现在允许您[自助生成和管理域验证 (DV) SSL 证书。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 这可为您提供最快捷、最简单、最具成本效益的解决方案，从而为您的在线业务创建一个安全的网站。

如果您有兴趣测试这项新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向 `Grp-aemcs-dv-dert-adopter@adobe.com` 发送一封电子邮件。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？若要开始使用，请从与您的 Adobe ID 关联的电子邮件发送电子邮件至 `aem-lighthouse-pilot@adobe.com`。
