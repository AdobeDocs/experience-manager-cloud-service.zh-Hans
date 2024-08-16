---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.8.0 的发行说明
description: 了解AEM as a Cloud Service中的Cloud Manager 2024.8.0发行说明。
feature: Release Information
role: Admin
source-git-commit: a823bcd1461b847983d0243cd9abd59efd8d7b6f
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 26%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2024.8.0发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.8.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.8.0版的发布日期是2024年8月14日。 下一个版本计划于2024年9月14日发布。

## 新增功能 {#what-is-new}

* [其他发布区域](/help/operations/additional-publish-regions.md)和[99.99%的SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)（服务水平协议）现在可用于AEM Formsas a Cloud Service。
   * 此增强功能允许您通过增加正常运行时间和减少延迟来实现更高的SLA，从而确保为遍布全球的用户提供同类最佳的体验。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### Cloud Manager中的Edge Delivery Services支持 {#edge-delivery-services}

如果您已将Edge Delivery Services作为AEM Sites的一部分授予许可，则[您现在可以直接在Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md)中使用Edge Delivery Services载入您的网站，并使用引导式自助服务体验上线。

此功能可为您的所有AEM资产提供统一的体验。 它确保域名管理、SSL证书管理和CDN映射等关键工作流之间的一致性。

如果您有兴趣测试这项新功能并分享您的反馈，请从与您的Adobe ID关联的电子邮件地址向`aemcs-cmedgedelsvs-program-adopter@adobe.com`发送电子邮件。

### 域验证(DV)证书

使用Cloud Manager，您现在可以[自助生成和管理域验证(DV) SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)。 此功能为您提供了最快、最简单、最经济高效的解决方案，可为您的在线业务创建安全的网站。

如果要测试这项新功能并提供反馈，请使用链接到Adobe ID的电子邮件地址向`Grp-aemcs-dv-dert-adopter@adobe.com`发送电子邮件。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以使用它审核任何网页，无论是公共网页还是需要身份验证的网页。 它提供对性能、可访问性、渐进式Web应用程序、SEO等的评估。

想试试新仪表板？ 若要开始，请使用链接到Adobe ID的电子邮件向`aem-lighthouse-pilot@adobe.com`发送电子邮件。

## 错误修复

* 删除管道后，发现管道步骤正在运行，此问题现已罕见地得以纠正。
* 已修复配置管道在极少数情况下错误显示`FAILED`状态的问题。
