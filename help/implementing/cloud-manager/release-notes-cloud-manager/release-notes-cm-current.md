---
title: Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.3.0的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 0749099acf98b09d0f83bfe86c2cc4558261c029
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明 {#release-notes}

本页记录了AEMas a Cloud Service中Cloud Manager 2022.3.0的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM 2022年3月10日as a Cloud Service的Cloud Manager 2022.3.0版的发布日期。 下一版本计划于2022年4月7日发布。

## 新增功能 {#what-is-new}

* 使用开发人员角色可以访问AEM环境日志。

## 错误修复 {#bug-fixes}

* 手动创建的git存储库的子集具有不正确的名称值，这会阻止生成对象重用功能生效。 这些存储库的名称已更改，用户将在Cloud Manager API/UI中看到更正的名称。
* 非生产管道的人造物在生产全堆流水线上被不当地重复使用。
* 添加或编辑代码质量管道时，不再显示用于处理量度失败的选项。
* 在生成步骤中，可能会导致一些意外的管道变量配置。
