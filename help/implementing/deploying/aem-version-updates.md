---
title: AEM版本更新
description: 'AEM版本更新 '
feature: 部署
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# AEM版本更新{#aem-version-updates}

## 简介 {#introduction}

AEM as aCloud Service现在使用连续集成和连续交付(CI/CD)来确保您的项目处于最新的AEM版本。 这意味着，Production和Stage实例将更新到最新的AEM版本，而不会中断用户的服务。

>[!NOTE]
>如果对生产环境的更新失败，Cloud Manager将自动回滚暂存环境。 此操作会自动完成，以确保更新完成后，暂存环境和生产环境都位于同一AEM版本上。

AEM版本更新有两种类型：

* **AEM推送更新**

   * 可以每天发布。

   * 主要是维护，包括最新的错误修复和安全更新。

      由于更改会定期应用，因此影响会是递增的，从而减少对服务的影响。

* **新增功能更新**

   * 通过可预测的每月计划发布。

AEM更新通过密集且完全自动化的产品验证管道，涉及多个步骤，以确保生产中任何系统的服务不会中断。 运行状况检查用于监控应用程序的运行状况。 如果在AEM as a Cloud Service更新期间，这些检查失败，则该版本将不继续，并且Adobe将调查更新为何会导致此意外行为。

[在AEM版本更新期间，](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) 还会验证阻止产品升级和客户代码推送中断生产的产品测试和客户功能测试。

>[!NOTE]
>
>如果自定义代码被推送到暂存环境，然后被您拒绝，则下次AEM更新将删除这些更改，以将上次成功客户版本的git标记反映到生产环境中。

## 复合节点存储{#composite-node-store}

如上所述，在大多数情况下，更新将导致零停机时间，包括作者（即节点群集）。 由于Oak中的&#x200B;*复合节点存储*&#x200B;功能，可能会进行滚动更新。

此功能允许AEM同时引用多个存储库。 在滚动部署中，新的绿色AEM版本包含其自己的`/libs`（基于TarMK的不可变存储库），它与旧的蓝色AEM版本不同，不过这两个版本都引用了基于DocumentMK的共享可变存储库，该存储库包含`/content` 、 `/conf` 、 `/etc`等区域。 由于蓝色和绿色都有其各自的`/libs`版本，因此在滚动更新期间，它们都可以处于活动状态，直到蓝色完全被绿色替换为止，它们都会占用流量。
