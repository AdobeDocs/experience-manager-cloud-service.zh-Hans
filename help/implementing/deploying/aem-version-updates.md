---
title: AEM 版本更新
description: 'AEM 版本更新 '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 36%

---

# AEM 版本更新 {#aem-version-updates}

## 简介 {#introduction}

AEM as a Cloud Service 现在使用连续集成和连续交付 (CI/CD)，以确保您的项目使用的是最新的 AEM 版本。这意味着生产实例和暂存实例均会更新到最新 AEM 版本而无需中断用户的服务。

>[!NOTE]
>如果对生产环境的更新失败，Cloud Manager 将自动回滚到暂存环境。此操作自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个 AEM 版本。

AEM 版本更新分为两种类型：

* **AEM 推送更新**

   * 可以每日发布。

   * 主要是用于维护，包括最新的错误修复和安全更新。

      由于定期应用更改，因此其影响是增量式的，因此减少了对您服务的影响。

* **新增功能更新**

   * 按照可预测的每月计划发布。

AEM更新通过密集且完全自动化的产品验证管道，涉及多个步骤，以确保生产中任何系统的服务不会中断。 运行状况检查用于监控应用程序的运行状况。 如果这些检查在AEMas a Cloud Service更新期间失败，则该版本将不继续，并且Adobe将调查更新为何会导致此意外行为。

[产品测试和客户功能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) 在AEM版本更新期间，还会验证阻止产品升级和客户代码推送中断生产的功能。

>[!NOTE]
>
>如果自定义代码被推送到暂存环境，然后被您拒绝，则下次AEM更新将删除这些更改，以将上次成功客户版本的git标记反映到生产环境中。

## 复合节点存储 {#composite-node-store}

如上所述，在大多数情况下，更新将导致零停机时间，包括作者（即节点群集）。 由于 *复合节点存储* 功能。

此功能允许AEM同时引用多个存储库。 在滚动部署中，新的绿色AEM版本包含其自己的 `/libs` （基于TarMK的不可变存储库），与旧的蓝色AEM版本不同，不过这两个存储库都引用了一个基于DocumentMK的共享可变存储库，其中包含以下区域： `/content` , `/conf` , `/etc` 等等。 因为蓝色和绿色都有各自的版本 `/libs`，则它们在滚动更新期间均可处于活动状态，在蓝色完全替换为绿色之前都会占用流量。
