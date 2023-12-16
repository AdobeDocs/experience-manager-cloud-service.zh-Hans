---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.12.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.12.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: c0fc4b2ced046a1e975aca99463cdfa03462f2f4
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 54%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.12.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2023.12.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中的Cloud Manager 2023.12.0版的发布日期为2023年12月14日。 下一个版本计划于 2024 年 1 月 18 日发布。

## 新增功能 {#what-is-new}

* [Cloud Manager 自定义权限](/help/implementing/cloud-manager/custom-permissions.md)可让您创建具有可配置权限的自定义权限配置文件，以限制 Cloud Manager 用户对项目、管道和环境的访问。
   * 此功能将分阶段推出，预计2024年2月发布的Cloud Manager将分阶段完成。
   * 请发送电子邮件至 `Grp-CloudManager-custom-permissions@adobe.com` 从与Adobe ID关联的电子邮件地址启用（如果您希望更早启用）。
* 现在，生成容器支持用于以下项的Node.js版本18： [前端管道。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* 对于新创建的Cloud Manager程序， [关联的New Relic子帐户](/help/implementing/cloud-manager/user-access-new-relic.md) 默认情况下不激活。
   * 对于超过90天未访问New Relic子帐户的现有程序，将停用该帐户。
   * 如果您希望使用New Relic子帐户，则需要通过Cloud Manager选择加入。
* 将更新转出到 [构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 曾经是 [宣布并从10月发布的Cloud Manager开始](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) 已完成。
   * 添加了对节点18的支持 [前端管道和全栈管道。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)
   * Java 8次要版本已更新为 `jdk1.8.0_371`.
   * Java 11次要版本已更新为 `jdk-11.0.20`.
   * Maven已更新至版本3.8.8。
      * Maven现在禁用所有不安全的内容 `http://*` 默认镜像。
      * [Adobe推荐](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 用户更新其Maven存储库以使用HTTPS而不是HTTP。
   * 构建容器基础图像已更新为Ubuntu 22.04。

## 早期采用计划 {#early-adoption}

加入 Adobe 早期采用计划，即有机会测试一些即将推出的功能。

### 通过Real User Monitoring (RUM)进行客户端收集 {#rum}

您可以利用 [Real User Monitoring (RUM)数据服务](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) 为AEMas a Cloud Service启用客户端收集。

Real User Monitoring (RUM) Data Service提供了对用户交互的更精确反映，从而确保了对网站参与情况的可靠衡量。 这是深入了解您的页面性能的绝佳机会。 这对使用Adobe托管的CDN或非Adobe托管的CDN的客户是有益的。 对于使用非Adobe托管CDN的客户，现在可以为其启用自动流量报表，因此无需与Adobe共享任何流量报表。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `aemcs-rum-adopter@adobe.com` 来自与您的Adobe ID关联的电子邮件地址。 请在您的电子邮件中包含用于生产、暂存和开发环境的域名。  此功能的早期采用者计划的可用性是有限的。

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/implementing/cloud-manager/managing-code/byo-github.md)此集成使您无需始终与 Adobe 存储库同步代码，并可在将拉取请求合并到主分支之前对其进行验证。

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。

### 自助内容恢复 {#content-restore}

[新的自助内容恢复功能](/help/operations/restore.md)现在提供长达 7 天的备份恢复，并可供早期采用者用于评估目的，其中包括：

* 前 24 小时的时间点备份恢复
* 固定时间恢复最长可达 7 天

如果您有兴趣测试此新功能并分享您的反馈，请从您的 Adobe ID 关联的电子邮件发送电子邮件至 `aemcs-restorefrombackup-adopter@adobe.com`。

* 早期采用者计划仅限于开发环境。
* 此功能的早期采用者计划的可用性是有限的。
* 此功能用于恢复意外删除的内容，不适用于灾难恢复。

### 体验审核仪表板 {#experience-audit-dashboard}

[Cloud Manager 体验审核仪表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括页面性能分数的趋势视图以及帮助您改进的见解和推荐。体验审核作为 Cloud Manager 生产管道中的一个步骤包含在内。

该仪表板利用 Google Lighthouse，这是一种开源自动化工具，用于提高 Web 应用程序的质量。您可以针对任何网页（公共网页或需要身份验证的网页）运行它。它对性能、可访问性、SEO、搜索引擎优化等进行审核。

有兴趣试驾新仪表板吗？若要开始使用，请从与您的 Adobe ID 关联的电子邮件发送电子邮件至 `aem-lighthouse-pilot@adobe.com`。
