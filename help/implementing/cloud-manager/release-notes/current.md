---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 8d5d8910a906e2adf17fa9c75f17634602c2e0b9
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 50%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.6.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.6.0 版本的发布日期是 2024 年 6 月 6 日。下一个版本计划于 2024 年 7 月 11 日发布。

## 新增功能 {#what-is-new}

* 您现在可以 [使用您自己的GitHub存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md) 用作全栈管道和前端管道的源。
   * 此外，您还可以通过以下方式利用GitHub存储库 [Git子模块，](/help/implementing/cloud-manager/managing-code/git-submodules.md) 增强了对用于拉取请求验证的自动生成管道的控制，并允许您在代码扫描阶段定义关键量度的行为。
   * [您也可选择](/help/implementing/cloud-manager/managing-code/github-check-config.md) 要在GitHub上保留报表历史记录，请命名管道并设置管道变量以满足您的需求。
* [自助内容恢复](/help/operations/restore.md) 提供长达7天的备份恢复以及以下功能：
   * 前 24 小时的时间点备份恢复
   * 固定时间恢复最长可达 7 天
* [新的OakPal规则](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) 已添加到Cloud Manager代码质量扫描。
   * 截至2024年6月添加的每个新规则都是一个不中断的更改。
   * 我们建议您尽快解决这些问题，因为从2024年8月发行的Cloud Manager版本开始，这些新规则会导致管道失败。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### Cloud Manager中的Edge Delivery Services支持 {#edge-delivery-services}

如果您已将Edge Delivery Services作为Adobe Experience Manager Sites的一部分授予许可， [您现在可以直接在Cloud Manager中使用Edge Delivery Services载入您的站点](/help/implementing/cloud-manager/edge-delivery-services.md) 使用引导式自助服务体验上线。

这可以为所有AEM资产实现统一的体验，确保与所有关键工作流程（包括域名管理、SSL证书管理和CDN映射）的一致性。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `aemcs-cmedgedelsvs-program-adopter@adobe.com` 来自与您的Adobe ID关联的电子邮件地址。

### 域验证(DV)证书

Cloud Manager现在允许您 [自助服务生成和管理域验证(DV) SSL证书。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 这为您提供了最快、最简单、最经济高效的解决方案，可为您的在线业务创建安全的网站。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `Grp-aemcs-dv-dert-adopter@adobe.com` 来自与您的Adobe ID关联的电子邮件地址。

### 通过实时监控(RUM)进行客户端收集 {#rum}

您可以利用 [Real Use Monitoring (RUM)数据服务](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) 为AEMas a Cloud Service启用客户端收集。

Real Use Monitoring (RUM) Data Service提供了对用户交互的更精确的反映，从而确保了对网站参与度的可靠衡量。 这是一个深入了解页面性能的绝佳机会。这对于使用 Adobe 管理的 CDN 或非 Adobe 管理的 CDN 的客户都很有用。对于使用非 Adobe 管理的 CDN 的客户，现在可为其启用自动流量报告，这样即无需与 Adobe 共享任何流量报告。

如果您有兴趣测试这项新功能并共享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址向 `aemcs-rum-adopter@adobe.com` 发送一封电子邮件。请在您的电子邮件中包含生产、暂存和开发环境的域名。参与此功能的早期采用者计划的人数受限。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？若要开始使用，请从与您的 Adobe ID 关联的电子邮件发送电子邮件至 `aem-lighthouse-pilot@adobe.com`。
