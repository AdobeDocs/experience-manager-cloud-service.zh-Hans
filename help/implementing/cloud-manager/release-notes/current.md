---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 37%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中的Cloud Manager 2023.6.0版的发布日期是2023年6月8日。 下一个版本计划于2023年7月6日发布。

## 新增功能 {#what-is-new}

* 创建新时 [项目或环境，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 现在，该名称仅接受字母数字字符和一组有限的特殊字符。
* 恢复时 [生产管道，](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 现在，批准步骤中会显示确认对话框。
* 对于 **[客户功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** 和 **[自定义用户界面测试](/help/implementing/cloud-manager/ui-testing.md)** 管道步骤，新 `INCOMPLETE` 现在可以为status ，这表示此类测试不存在，因此未执行。
   * 在这种情况下，管道不会失败并进入下一步。

## 错误修复 {#bug-fixes}

* 此 [Web层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 不再错误地为仅用于Assets的项目启用。
* 添加了更强大的验证，以防止在环境预配期间出现某些类型的故障。
