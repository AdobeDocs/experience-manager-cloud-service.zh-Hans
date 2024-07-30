---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 12e19fe771c0b70ec471949944141f4d6858cbfd
workflow-type: ht
source-wordcount: '633'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.7.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.7.0 版本的发布日期是 2024 年 7 月 18 日。计划于 2024 年 8 月 8 日发布下一个版本。

## 新增功能 {#what-is-new}

* [生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)和[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline) 触发器 **On Git Changes** 可在提交时启动管道，现在可用于 [ 专用存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)。
   * 该计划将分阶段实施，并于 8 月中旬完成。
* 添加 [Adobe 管理的 DV 证书时，](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 您现在可以添加涵盖多个域的单个证书，而不必为每个域创建一个证书。
* 现在可以将没有 [附加发布区域](/help/operations/additional-publish-regions.md) 的解决方案添加到程序中，只要该程序至少有一个适用于它的 Sites 或 Forms 解决方案。
* 现在可以将不具备 [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) 的解决方案添加到程序中，只要该程序至少有一个适用于它的 Sites 或 Forms 解决方案。
*  [体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md) 已在许多方面得到增强。
   * 审核现在通过 CDN 针对 `.com` 端点运行，取代了以前的 `.net` 方法。
      * 这一变化更准确地模拟了真实的用户体验，并帮助您就管理和优化网站做出更明智的决策。
   * 体验审核 UI 进行了多项增强，包括：
      * 添加了性能、最佳实践、SEO 和可访问性的趋势视图。
      * Lighthouse 原始报告链接现在可以以更直观的方式直接显示在扫描快照详细信息面板中。
      * Lighthouse 建议部分已得到增强。
   * 根据 Lighthouse 12.0.0 版本，PWA 指标已被删除，从而取消了这个指标。
* [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)已更新到[版本 49。](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49)

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
