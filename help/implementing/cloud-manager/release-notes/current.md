---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: deef27dd90be22669b2328f6e394b8d3df99b4b9
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.6.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.6.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2023.6.0 版本的发布日期是 2023 年 6 月 8 日。下一个版本计划于 2023 年 7 月 6 日发布。

## 新增功能 {#what-is-new}

* 除了主要区域之外，客户还可以购买额外的次要发布区域，从而获得减少延迟和提高可用性等方面的好处。注释：可能存在某些限制。
* 创建新的[程序或环境时，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)名称现在仅限于接受字母数字字符和一组有限的特殊字符。
* 当恢复[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)时，现在在批准步骤中会显示一个确认对话框。
* 对于&#x200B;**[客户功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)**&#x200B;和&#x200B;**[自定义 UI 测试](/help/implementing/cloud-manager/ui-testing.md)**&#x200B;管道步骤，现在可能出现新的 `INCOMPLETE` 状态，这表明此类测试不存在，因此未执行。
   * 在这种情况下，管道不会出现故障，并会进入下一步。

## 错误修复 {#bug-fixes}

* [Web 层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)不再为仅资源程序以错误的方式启用。
* 添加了更强大的验证功能，以防止在环境配置期间出现某些类型的故障。
