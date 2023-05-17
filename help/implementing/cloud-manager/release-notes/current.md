---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: ht
source-wordcount: '206'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.5.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 2023.5.0 中的 Cloud Manager 的发布日期是 2023 年 5 月 11 日。下一个版本计划于 2023 年 6 月 8 日发布。

## 新增功能 {#what-is-new}

* 产品、功能和 UI 测试支持已扩大至[非生产管道测试](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。
* 除了启用测试上游之外，[UI 测试支持已扩大至 Cypress 测试。](/help/implementing/cloud-manager/ui-testing.md)
* 现在可通过 Cloud Manager UI 从较高环境向较低环境执行[自助内容复制](/help/implementing/developing/tools/content-copy.md)。
* 已增强管道执行验证步骤，以便在执行过程中的早期验证复制队列的状态。这样确保部署步骤不受队列被阻塞的影响，应由 AEM 管理员用户直接在创作环境中解决阻塞问题。

## 错误修复 {#bug-fixes}

* 在环境的名称中使用多字节字符时创建环境不再失败。
