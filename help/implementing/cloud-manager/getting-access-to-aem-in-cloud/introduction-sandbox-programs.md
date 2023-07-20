---
title: 沙盒程序简介
description: 了解沙盒程序与生产程序的区别。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 100%

---


# 沙盒程序简介 {#sandbox-programs}

了解沙盒程序与生产程序的区别。

## 简介 {#introduction}

沙盒程序通常是为了满足培训、运行演示、启用或概念验证 (POC) 的目的而创建的，因此不会承载实时流量。

沙盒程序是 AEM Cloud Service 中可用的两种程序之一，另一种是[生产程序。](introduction-production-programs.md)请参阅[了解程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)，以了解有关程序类型的更多信息。

## 自动创建 {#auto-creation}

沙盒程序具有自动创建功能。 每当您自动创建新的沙盒程序 Cloud Manager 时：

* 在程序中添加 AEM Sites 和 AEM Assets 作为解决方案。
* 使用基于 [AEM 项目原型的示例项目设置项目 git 存储库。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* 创建开发环境。
* 创建部署到开发环境的非生产管道。

沙盒程序将只有一个开发环境。

## 限制和条件 {#limitations}

因为沙盒程序不适合实时流量，所以其使用有一定的限制和条件，这使得沙盒程序与生产程序不同。

### 无实时流量 {#live-traffic}

沙盒程序不会承载实时流量，因此不受 [AEM as a Cloud Service 承诺的约束。](https://www.adobe.com/cn/legal/service-commitments.html)

### 无自动缩放 {#auto-scaling}

在沙盒程序中创建的环境未配置为自动缩放。 因此，这些环境不适合进行性能或负载测试。

### 没有自定义域或 IP 允许列表 {#ip-allow}

自定义域和 IP 允许列表在沙盒程序中不可用。

### 无高级网络 {#advanced-networking}

[高级网络功能](/help/security/configuring-advanced-networking.md)（例如 VPN、非标准端口、专用出口 IP 地址的自助供应等） 在沙盒程序中不可用。

### 手动 AEM 更新 {#updates}

AEM 更新不会自动推送到沙盒程序，但可以手动应用到沙盒程序中的环境。

* 只有目标环境具有正确配置的管道时，才能运行手动更新。
* 手动更新生产环境或暂存环境将自动更新其他环境。生产 + 暂存环境集必须位于同一 AEM 版本上。

有关更多详细信息，请参阅 [AEM 版本更新。](/help/implementing/deploying/aem-version-updates.md)

请参阅[更新环境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)了解具体操作步骤。

### 休眠和删除 {#hibernation}

沙盒程序中的环境在八小时不活动后自动休眠。沙盒环境在连续休眠六个月后将被删除。

请参阅[沙盒环境休眠和解除休眠](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)以了解有关如何解除环境休眠和自动删除沙箱的更多详细信息。

### 无技术支持 {#no-support}

由于创建沙盒程序的目的通常是培训、运行演示、启用或概念验证 (POC)，因此无法为沙盒程序中遇到的问题提供技术支持。

如果您在创建和管理沙盒程序时遇到问题，这仍在技术支持范围内。
