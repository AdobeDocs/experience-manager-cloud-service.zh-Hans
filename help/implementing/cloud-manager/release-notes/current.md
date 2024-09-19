---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2024.9.0 发行说明。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.9.0 版本的发行说明。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2024.9.0 的发布日期是 2024 年 9 月 5 日。下一个版本计划于 2024 年 10 月 3 日发布。

## 新增功能 {#what-is-new}

* **体验审核仪表板**

  Adobe Cloud Manager 的[增强型体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)由 Google Lighthouse 提供支持，可通过评估核心网络生命力、SEO 和可访问性量度，提供有关 AEM Sites 质量和性能的见解。它通过提供可行的建议帮助用户确定需要改进的领域，使团队能够增强用户体验、页面加载时间和网站合规性。该仪表板简化了对重要网站量度的监控，并确保 AEM 应用程序能够满足性能和可访问性方面的高标准。

* **Adobe 生成和管理的域验证证书：**

  借助 Cloud Manager，您现在可以[自助使用 Adobe 生成和管理的 DV（域验证）SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。此功能为您提供最快捷、最简单、最具成本效益的解决方案，为您的在线组织或业务创建一个安全的网站。<!-- CMGR-52403 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md) 客户计划分阶段逐步推出此功能。

* **Cloud Manager 中的 Edge Delivery Services 支持：**

  如果您在 AEM Sites 中具有 Edge Delivery Services 许可证，[您现在可以直接通过 Cloud Manager 在您的网站中加入 Edge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。此功能可实现引导式、自助式的 Go Live 体验。它还统一了所有 AEM 属性中的域名管理、SSL 证书和 CDN 映射等基本工作流程，确保实现一致性和高效率。<!-- CMGR-49859 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md) 客户计划分阶段逐步推出此功能。

* 使用 GitHub 存储库的客户现在可以创建和使用 Web Tier Config 管道。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## 错误修复

* SSL 证书表视图的分页功能现在可以正常工作。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 使用执行中的&#x200B;**提升版本**&#x200B;按钮时提升的工件版本有误。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
