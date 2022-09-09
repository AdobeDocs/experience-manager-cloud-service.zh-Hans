---
title: Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.3.0的发行说明。
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 52%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.3.0发行说明 {#release-notes}

本页记录了AEMas a Cloud Service中Cloud Manager 2022.3.0的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2022.3.0版的发布日期是2022年3月10日。 下一版本计划于2022年4月7日发布。

## 新增功能 {#what-is-new}

* 可以使用开发人员角色访问 AEM 环境日志。

## 错误修复 {#bug-fixes}

* 手动创建的 Git 存储库的一个子集的名称值不正确，这使得生成工件的重用功能无法生效。这些存储库的名称已经更改，用户将在 Cloud Manager API/UI 中看到正确的名称。
* 来自非生产管道的生成工件不适当地重新用于生产全堆栈管道。
* 添加或编辑代码质量管道时，不再显示处理度量失败的选项。
* 一些意外的管道变量配置可能会在生成步骤中导致错误。
