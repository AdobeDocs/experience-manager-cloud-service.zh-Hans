---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的发行说明
description: 了解AEM as a Cloud Service中的Cloud Manager 2024.9.0发行说明。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 610ae004b6da2f7fc0dae2baa613cb363fe9fb00
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 13%

---

# Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2024.9.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.9.0 版本的发行说明。

>[!NOTE]
>
>请参阅[当前的Adobe Experience Manager as a Cloud Service发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发布日期 {#release-date}

AEM as a Cloud Service 2024.9.0版Cloud Manager的发布日期为2024年9月5日。 下一个版本计划于2024年10月3日发布。

## 新增功能 {#what-is-new}

* **体验审核仪表板：**

  AdobeCloud Manager的[增强型体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)(由Google Lighthouse提供支持)通过评估核心Web动态、SEO和可访问性指标，提供了对AEM Sites质量和性能的见解。 它通过提供切实可行的建议，帮助用户识别需要改进的方面，使团队能够增强用户体验、页面加载时间和网站合规性。 此仪表板简化了关键网站量度的监控，并确保AEM应用程序符合高性能和可访问性标准。

* **Adobe生成和管理的域验证证书：**

  使用Cloud Manager，您现在可以[生成和托管的DV(域Adobe)SSL证书的自助服务](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 此功能为您提供了最快、最简单、最经济高效的解决方案，可为您的在线组织或业务创建安全的网站。<!-- CMGR-52403 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md)客户计划在逐步推出过程中分阶段接收此功能。

* Cloud Manager中的&#x200B;**Edge Delivery Services支持：**

  如果您在AEM Sites中拥有Edge Delivery Services许可证，[您现在可以直接通过Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md)使用Edge Delivery Services载入您的网站。 此功能可提供引导式自助上线体验。 它还跨所有AEM资产统一域名管理、SSL证书和CDN映射等基本工作流，确保一致性和效率。<!-- CMGR-49859 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md)客户计划在逐步推出过程中分阶段接收此功能。

* 现在，使用GitHub存储库的客户能够创建和使用Web层配置管道。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## 错误修复

* 对SSL证书表格视图进行分页现在可按预期工作。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 从执行中使用&#x200B;**Promote Build**&#x200B;按钮时提升了错误的工件版本。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
