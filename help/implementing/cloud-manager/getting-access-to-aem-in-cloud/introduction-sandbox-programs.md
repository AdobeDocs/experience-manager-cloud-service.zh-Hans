---
title: '沙盒程序简介 '
description: 了解与生产程序有何不同的沙盒程序。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: b74a0dbb1c9fdb74941f7b71bed9215853b63666
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# 沙盒程序简介 {#sandbox-programs}

了解与生产程序有何不同的沙盒程序。

## Communications API {#introduction}

沙盒项目通常用于提供培训、运行演示、支持或概念验证(POC)目的，因此不能用于传输实时流量。

沙盒项目是AEM Cloud Service中可用的两种类型的项目之一，另一种是 [生产计划。](introduction-production-programs.md) 请参阅该文档 [了解程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 了解有关程序类型的更多信息。

## 自动创建 {#auto-creation}

沙盒程序具有自动创建功能。 每当您自动创建新的沙盒项目时，Cloud Manager都会：

* 将AEM Sites和AEM Assets作为解决方案添加到您的计划中。
* 设置项目git存储库，其中包含基于 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* 创建开发环境。
* 创建部署到开发环境的非生产管道。

沙盒项目将只有一个开发环境。

## 限制和条件 {#limitations}

由于沙盒程序不适用于实时流量，因此对于它们的使用存在某些限制和条件，这会将它们与生产程序区分开来。

### 无实时流量 {#live-traffic}

沙盒程序不用于传输实时流量，因此不受 [AEMas a Cloud Service承诺。](https://www.adobe.com/legal/service-commitments.html)

### 无自动缩放 {#auto-scaling}

在沙盒项目中创建的环境未配置为自动缩放。 因此，这些环境不适合进行性能或负载测试。

### 无自定义域或IP允许列表 {#ip-allow}

自定义域和IP允许列表在沙盒项目中不可用。

### 手动AEM更新 {#updates}

AEM更新不会自动推送到沙盒程序，但可以手动应用于沙盒程序中的环境。

* 只有在目标环境具有正确配置的管道时，才能运行手动更新。
* 手动更新生产或暂存环境将自动更新另一个环境。 生产+暂存环境集必须位于同一AEM版本上。

请参阅该文档 [AEM版本更新](/help/implementing/deploying/aem-version-updates.md) 以了解更多详细信息。

请参阅该文档 [更新环境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) 了解如何更新环境。

### 休眠和删除 {#hibernation}

沙盒项目中的环境在处于不活动状态8小时后会自动休眠。 休眠后，可以手动解除休眠。

沙盒项目在处于连续休眠模式6个月后被删除，之后可以重新创建它们。

请参阅 [休眠和解除休眠沙盒环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) 以了解更多详细信息。
