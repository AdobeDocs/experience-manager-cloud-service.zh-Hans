---
title: Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.3.0的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明 {#release-notes}

本页记录了AEMas a Cloud Service中Cloud Manager 2022.3.0的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM 2022年3月10日as a Cloud Service的Cloud Manager 2022.3.0版的发布日期。 下一版本计划于2022年4月7日发布。

## 新增功能 {#what-is-new}

* 具有 **开发人员** 角色现在可以访问AEM环境日志。
* [的 `reliability_rating` 关键量度](/help/implementing/cloud-manager/code-quality-testing.md) 已被禁用。
* 用户现在可以对 **管道** 页面。

## 错误修复 {#bug-fixes}

* 手动创建的Git存储库的子集具有不正确的名称值，这会影响 [构建对象重用功能。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 这些存储库的名称已更改，用户将在Cloud Manager API/UI中看到更正的名称。
* [添加或编辑代码质量管道时，](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) the **重要量度失败行为** 选项。
* 意外的管道变量配置不再导致生成步骤出错。
