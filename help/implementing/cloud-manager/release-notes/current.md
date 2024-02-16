---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.2.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2024.2.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4a41de9da557be562bb2ff5773c7954f76a9acc7
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 83%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.2.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.2.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.2.0 版本的发布日期是 2024 年 2 月 15 日。下一个版本计划于 2024 年 3 月 16 日发布。

## 新增功能 {#what-is-new}

* Cloud Manager现在支持以下项目的自助服务管理 [管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 通过Cloud Manager UI。
* [预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-sevice) 现在将为转出预览服务功能之前创建的环境启用。
* 通过 [Cloud Manager 自定义权限](/help/implementing/cloud-manager/custom-permissions.md)，可创建具有可配置的权限的自定义权限配置文件，以限制 Cloud Manager 用户对项目、管道和环境的访问。
   * 此功能开始分阶段推出 [2023年12月版](/help/implementing/cloud-manager/release-notes/2023/2023-12-0.md) 并将于2024年2月20日完成。
* 对于所有新环境， [环境产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md) 名称格式将更加便于用户使用，它以配置文件描述、环境类型、编号和项目编号的组合为基础。
* [构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 已更新至Maven版本3.9.4和JDK版本jdk-11.0.22和jdk1.8.0_401。

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

* 内部版本容器的JDK已更新到可以解决此问题的版本 [JDK-8313765。](https://bugs.openjdk.org/browse/JDK-8313765)
