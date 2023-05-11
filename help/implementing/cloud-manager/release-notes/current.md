---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 41%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.5.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.5.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2023.5.0版的发布日期是2023年5月11日。 下一个版本计划于 2023 年 6 月 8 日发布。

## 新增功能 {#what-is-new}

* 产品、功能和UI测试支持已扩展到 [非生产管道测试。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
* 除了启用上游测试外， [UI测试支持已扩展到Cypress测试。](/help/implementing/cloud-manager/ui-testing.md)
* [自助内容副本](/help/implementing/developing/tools/content-copy.md) 现在，可通过Cloud Manager UI从较高环境访问到较低环境。
* 管道执行验证步骤已得到增强，可在执行过程早期验证复制队列的状态。 这可确保部署步骤不受阻止队列的影响，这些队列应由AEM管理员用户直接在创作环境中解决。

## 错误修复 {#bug-fixes}

* 在环境名称中使用多字节字符时，环境创建不再失败。
